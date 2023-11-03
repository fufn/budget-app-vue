<template>
  <div class="budget-list-wrap">
    <el-card :header="header">
      <template v-if="!isEmpty">
        <el-button class="my-button" @click="sortValues"> Sort </el-button>
        <el-button class="my-button" @click="showAll"> All </el-button>
        <el-button class="my-button" @click="showIncome"> Income </el-button>
        <el-button class="my-button" @click="showOutcome"> Outcome </el-button>
        <div v-for="(item, index) in list" :key="index">
          <BudgetListItem
            :item="item"
            :sortType="sortType"
            @deleteItem="onDeleteItem"
          />
        </div>
      </template>
      <el-alert
        v-else
        type="info"
        :title="emptyTitle"
        :closable="false"
      ></el-alert>
    </el-card>
  </div>
</template>

<script>
import BudgetListItem from "./BudgetListItem.vue";

export default {
  name: "BudgetList",
  components: {
    BudgetListItem,
  },
  props: {
    list: {
      type: Object,
      default: () => ({}),
    },
  },
  data: () => ({
    header: "Budget lsit",
    emptyTitle: "Empty List",
    dialogVisible: true,
    sortType: "all",
  }),
  computed: {
    isEmpty() {
      return !Object.keys(this.list).length;
    },
  },
  methods: {
    onDeleteItem(id) {
      console.log(`In Budget List ${id}`);
      this.$emit("deleteItem", id);
    },
    showAll() {
      this.sortType = "all";
    },
    showIncome() {
      this.sortType = "INCOME";
    },
    showOutcome() {
      this.sortType = "OUTCOME";
    },
  },
};
</script>

<style scoped>
.budget-list-wrap {
  max-width: 500px;
  margin: auto;
}
.my-button {
  max-width: 100px;
  width: 100%;
}
</style>
