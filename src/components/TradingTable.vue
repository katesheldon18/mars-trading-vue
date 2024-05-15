<script>
import Counter from "./Counter.vue";

export default {
  name: "TradingTable",
  components: {
    Counter,
  },
  data() {
      return {
          tableData: [],
    };
  },
  methods: {
    async fetchData() {
      try {
        const response = await fetch("https://www.blackpepper.co.nz/api/martian");
        this.tableData = await response.json();
        console.log(this.tableData);
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    },
    },
    mounted() {
        this.fetchData();
  }
};
</script>

<template>
  <div class="container">
    <Counter :initialCount="0" />
    <div>{{ tableData }}</div>
    <table>
      <div class="traders"></div>
      <thead>
        <tr>
          <td>Hello world heading</td>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Hello world cells</td>
        </tr>
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
