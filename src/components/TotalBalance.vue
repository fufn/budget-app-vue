<template>
  <div class="total-value" :style="getColor">Balance : {{ total }}</div>
</template>

<script>
export default {
  name: "TotalBalance",
  props: {
    total: {
      type: Number,
      default: 0,
    },
  },
  data: () => ({
    color: "#ff0000",
  }),
  computed: {
    getColor() {
      if (this.total < 0) {
        return "color: #ff0000";
      } else if (this.total > 0) {
        return "color: #008000";
      } else {
        return "color: #000000";
      }
    },
  },
};
</script>

<style scoped>
.total-value {
  font-size: 26px;
  text-transform: uppercase;
  padding: 20px;
  text-align: center;
}
</style>
