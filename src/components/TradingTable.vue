<script>
import Counter from './Counter.vue';

export default {
  name: 'TradingTable',
  components: {
    Counter
  },
  data() {
    return {
      headers: ['Header 1', 'Header 2', 'Header 3', 'Header 4', 'Header 5', 'Header 6', 'Header 7'],
      tableData: [
        ['Oxygen', 'Oxygen', 'Oxygen'],
        ['Oxygen', 'Oxygen', 'Oxygen'],
        ['Oxygen', 'Oxygen', 'Oxygen'],
        ['Oxygen', 'Oxygen', 'Oxygen'],
        ['Oxygen', 'Oxygen', 'Oxygen'],
        ['Oxygen', 'Oxygen', 'Oxygen'],
        ['Total', 0, 0]
      ]
    };
  }
};
</script>

<template>
    <div class="container">
        <Counter :initialCount="0"/>
        <table>
            <div class="traders"></div>
            <tbody>
                <tr v-for="(row, rowIndex) in tableData" :key="rowIndex">
                    <td v-for="(cell, cellIndex) in row" :key="cellIndex">{{ cell }}</td>
                </tr>
            </tbody>
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

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
