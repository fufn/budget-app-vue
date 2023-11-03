<template v>
  <div class="list-item" v-if="checkType">
    <el-icon :color="getColor" v-if="getDirection">
      <Top />
    </el-icon>
    <el-icon :color="getColor" v-else>
      <Bottom />
    </el-icon>
    <span class="budget-comment">{{ item.comment }}</span>
    <span class="budget-value">{{ item.value }}</span>
    <el-button type="danger" size="mini" @click="deleteItem(item.id)"
      >Delete</el-button
    >
  </div>
</template>

<script>
export default {
  name: "BudgetListItem",
  props: {
    item: {
      type: Object,
      required: true,
      default: () => ({}),
    },
    sortType: {
      type: String,
      required: true,
      default: "all",
    },
  },
  methods: {
    deleteItem(id) {
      if (!confirm()) return;
      this.$emit("deleteItem", id);
    },
  },
  computed: {
    getColor() {
      if (this.item.type === "INCOME") {
        return "green";
      } else {
        return "red";
      }
    },
    getDirection() {
      return this.item.type === "INCOME";
    },
    checkType() {
      if (this.sortType == "all") return true;
      return this.item.type === this.sortType;
    },
  },
};
</script>

<style scoped>
.budget-value {
  font-weight: bold;
  margin-left: auto;
  margin-right: 20px;
}

.list-item {
  display: flex;
  align-items: center;
  padding: 10px 15px;
}
</style>
