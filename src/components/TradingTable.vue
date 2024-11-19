<script>
import Counter from "./Counter.vue";

export default {
  name: "TradingTable",
  components: {
    Counter,
  },
  data() {
    return {
      tradingData: {},
      selectedTrader1: "",
      selectedTrader2: "",
    };
  },
  methods: {
    async fetchData() {
      try {
        const response = await fetch(
          "https://www.blackpepper.co.nz/api/martian"
        );
        this.tradingData = await response.json();
        console.log(this.tradingData);
      } catch (error) {
        console.error("Error fetching trading data:", error);
      }
    },
    async fetchItems() {
      try {
        const response = await fetch(
          "https://www.blackpepper.co.nz/api/martian/items"
        );
        this.itemData = await response.json();
        console.log(this.itemData);
      } catch (error) {
        console.error("Error fetching item data:", error);
      }
    },
  },
  computed: {
  trader1Items() {
    if (!this.selectedTrader1) return [];
    const trader = this.tradingData.data?.find(
      (trader) => trader.name === this.selectedTrader1
    );
    return trader ? trader.inventory : [];
  },
  trader2Items() {
    if (!this.selectedTrader2) return [];
    const trader = this.tradingData.data?.find(
      (trader) => trader.name === this.selectedTrader2
    );
    return trader ? trader.inventory : [];
  }
},
  mounted() {
    this.fetchData();
    this.fetchItems();
  },
};
</script>

<template>
  <div class="container">
    <h1 class="heading">MARS TRADING PLATFORM</h1>
    <div class="dropdown-container">
      <div class="dropdown-wrapper">
        <label for="dropdown1">Trader 1</label>
        <select class="dropdown" id="dropdown1" v-model="selectedTrader1">
          <option disabled hidden value="">Select</option>
          <option 
            v-for="trader in tradingData.data" 
            :key="trader.name"
            :disabled="trader.name === selectedTrader2"
            :value="trader.name">
            {{ trader.name }}
          </option>
        </select>
      </div>
      <div class="dropdown-wrapper">
        <label for="dropdown2">Trader 2</label>
        <select class="dropdown" id="dropdown2" v-model="selectedTrader2">
          <option disabled hidden value="">Select</option>
          <option 
            v-for="trader in tradingData.data" 
            :key="trader.name"
            :disabled="trader.name === selectedTrader1"
            :value="trader.name">
            {{ trader.name }}
          </option>
        </select>
      </div>
    </div>
    <table>
      <tbody>
        <tr v-for="(item, index) in itemData?.data" :key="item.name" :class="{'odd-row' : index % 2 !== 1}">
          {{
            item.name
          }}
          <td class="count"><Counter :maxCount="trader1Items[index]?.quantity || 0"/></td>
          <td class="count"><Counter :maxCount="trader2Items[index]?.quantity || 0"/></td>
        </tr>
      </tbody>
      <tfoot>
        <tr>
          <td>Total</td>
        </tr>
      </tfoot>
    </table>
    <div class="table-buttons">
      <button class="btn btn-reset">RESET</button>
      <button class="btn btn-trade">TRADE</button>
    </div>
  </div>
</template>

<style>
body {
  background-image: url('@/assets/bg.png');
  background-size: cover;
  background-position: center;
}
</style>

<style scoped>
h1 {
  font-weight: 700;
  font-size: 14px;
  line-height: 24px;
  letter-spacing: 2px;
}
.dropdown-container {
  display: flex;
  height: 5rem;
  align-items: center;
  gap: 0.5rem;
}
.dropdown-wrapper {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.dropdown-wrapper label {
  font-size: 0.75rem;
}
.dropdown {
  background-color: transparent;
  border: none;
  color: white;
  width: 12rem;
  font-size: 0.875rem;
}
table {
  border-collapse: collapse;
}
tr {
  vertical-align: initial;
}
.odd-row {
  background-color: #FFFFFF1A;
  opacity: 0.9;
}
.count {
  color: #7F7F7F;
  padding: 1.75rem 0;
}
.btn {
  font-size: 14px;
  font-weight: 700;
  line-height: 24px;
  letter-spacing: 2px;
  text-align: center;
  border-radius: 48px;
  padding: 8px 55px;
  margin: 48px;
  cursor: pointer;
}
.btn-reset {
  border: 1px solid #ffffff;
  background-color: transparent;
}
.btn-trade {
  border: 1px solid #7f7f7f;
  background-color: #7f7f7f;
  color: white;
}
</style>
