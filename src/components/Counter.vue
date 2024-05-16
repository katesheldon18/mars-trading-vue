<script>
export default {
  name: "Counter",
  props: {
    initialCount: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      count: this.initialCount,
    };
  },
  methods: {
    increment() {
      this.count++;
      this.$emit("updateCount", this.count);
    },
    decrement() {
      if (this.count > 0) {
        this.count--;
        this.$emit("updateCount", this.count);
      }
    },
  },
};
</script>

<template>
  <div class="container">
    <button class="change-count" @click="decrement">-</button>
    <span>{{ count }} / {{ count }}</span>
    <button class="change-count" @click="increment">+</button>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  align-items: center;
}
.change-count {
  border: 1px solid #808080;
  border-radius: 99%;
  background-color: transparent;
  cursor: pointer;
  margin: 8px;
}
</style>
