<script>
export default {
  name: 'Counter',
  props: {
    initialCount: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      count: this.initialCount
    };
  },
  methods: {
    increment() {
      this.count++;
      this.$emit('updateCount', this.count);
    },
    decrement() {
      if (this.count > 0) {
        this.count--;
        this.$emit('updateCount', this.count);
      }
    }
  }
};
</script>

<template>
    <div class="container">
      <button @click="decrement">-</button>
      <span>{{ count }}</span>
      <button @click="increment">+</button>
    </div>
</template>


<style scoped>
.container {
  display: flex;
  align-items: center;
}
button {
  width: 30px;
  height: 30px;
  margin: 0 5px;
}
span {
  width: 30px;
  text-align: center;
}
</style>