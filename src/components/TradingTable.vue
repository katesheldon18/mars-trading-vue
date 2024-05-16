<script>
import Counter from "./Counter.vue";

export default {
  name: "TradingTable",
  components: {
    Counter,
  },
  data() {
    return {
      tradingData: [],
      itemData: [],
      selectedTrader: "",
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
  mounted() {
    this.fetchData();
    this.fetchItems();
  },
};
</script>

<template>
  <div class="container">
    <h1 class="heading">MARS TRADING PLATFORM</h1>
    <div class="dropdowns">
      <div></div>
      <select>
        <option class="dropdown dropdown1">Select</option>
        <option v-for="trader in tradingData.data" :key="trader.name">
          {{ trader.name }}
        </option>
      </select>
      <select>
        <option class="dropdown dropdown1">Select</option>
        <option v-for="trader in tradingData.data" :key="trader.name">
          {{ trader.name }}
        </option>
      </select>
    </div>
    <table>
      <thead>
        <td></td>
        <td v-for="trader in tradingData.data" :key="trader.name">
          {{ trader.name }}
        </td>
      </thead>
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
.dropdowns {
  display: flex;
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
  margin: 0px 12px;
  cursor: pointer;
}
.btn-reset {
  /* border: 1px solid #ffffff; */
  border: 1px solid black;
  background-color: transparent;
}
.btn-trade {
  border: 1px solid #7f7f7f;
  background-color: #7f7f7f;
  color: white;
}
</style>
