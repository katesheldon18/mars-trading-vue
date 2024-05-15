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
    };
  },
  methods: {
    async fetchData() {
      try {
        const response = await fetch("https://www.blackpepper.co.nz/api/martian");
        this.tradingData = await response.json();
        console.log(this.tradingData);
      } catch (error) {
        console.error("Error fetching trading data:", error);
      }
      },
    async fetchItems() {
        try {
            const response = await fetch("https://www.blackpepper.co.nz/api/martian/items");
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
  }
};
</script>

<template>
    <div class="container">
        <Counter :initialCount="0" />
        <!-- <div>{{ tradingData }}</div>
        <div>{{ itemData.name }}</div> -->
        <!-- <div v-for="item in itemData.data" :key="item.name">{{ item.name }}</div> -->
        <table>
            <div class="traders"></div>
            <thead>
                <tr>
                    <td>Hello world heading</td>
                </tr>
            </thead>
            <tbody>
                <tr v-for="item in itemData.data" :key="item.name">{{ item.name }}</tr>
            </tbody>
            <tfoot>
                <tr>
                    <td>Total</td>
                </tr>
            </tfoot>
        </table>
    </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}
</style>
