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
      itemData: {},
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
    traderItems() {
      if (!this.selectedTrader) return [];
      const trader = this.tradingData.data.find(
        (trader) => trader.name === this.selectedTrader
      );
      if (!trader) return [];
      return trader.inventory.map((item) => item.quantity);
    },
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
      <select class="dropdown dropdown1" v-model="selectedTrader1">
        <option>Select</option>
        <option 
          v-for="trader in tradingData.data" 
          :key="trader.name"
          :disabled="trader.name === selectedTrader2"
          :value="trader.name">
          {{ trader.name }}
        </option>
      </select>
      <select class="dropdown dropdown2" v-model="selectedTrader2">
        <option>Select</option>
        <option 
          v-for="trader in tradingData.data" 
          :key="trader.name"
          :disabled="trader.name === selectedTrader1"
          :value="trader.name">
          {{ trader.name }}
        </option>
      </select>
    </div>
    <table>
      <tbody>
        <tr v-for="item in itemData.data" :key="item.name">
          {{
            item.name
          }}
          <td><Counter /></td>
          <td><Counter /></td>
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

<style scoped>
h1 {
  font-weight: 700;
  font-size: 14px;
  line-height: 24px;
  letter-spacing: 2px;
}
.dropdown {
  padding: 12px;
  margin: 12px;
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
