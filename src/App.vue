<template>
  <div>
    <FormVue @submitForm="onSubmitForm" />
    <TotalBalance :total="totalBalance"></TotalBalance>
    <BudgetList :list="list" @deleteItem="onDeleteItem"></BudgetList>
  </div>
</template>

<script>
import BudgetList from "./components/BudgetList.vue";
import TotalBalance from "./components/TotalBalance.vue";
import FormVue from "./components/Form.vue";

export default {
  name: "App",
  components: {
    BudgetList,
    TotalBalance,
    FormVue,
  },
  data: () => ({
    list: {
      1: {
        type: "INCOME",
        value: 100,
        comment: "Some comment",
        id: 1,
      },
      2: {
        type: "OUTCOME",
        value: -50,
        comment: "Some outcome comment",
        id: 2,
      },
    },
  }),
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce(
        (acc, item) => acc + item.value,
        0
      );
    },
  },
  methods: {
    onDeleteItem(id) {
      delete this.list[id];
    },
    onSubmitForm(form) {
      const newObject = {
        ...form,
        id: String(Math.random()),
      };
      this.list[newObject.id] = newObject;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
