<script>
export default {
  name: "Counter",
  data() {
    return {
      count: this.initialCount,
    };
  },
  props: {
    initialCount: {
      type: Number,
      default: 0
    },
    maxCount: {
      type: Number,
      required: true,
    },
  },
  methods: {
    increment() {
      if (this.count < this.maxCount) {
        this.count++;
      }
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
    <span>{{ count }} / {{ maxCount }}</span>
    <button class="change-count" @click="increment">+</button>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 129px;
}
.change-count {
  border: 1px solid #808080;
  color: #7F7F7F;

  border-radius: 99%;
  background-color: transparent;
  cursor: pointer;
  margin: 8px;
}
</style>
