<template>
  <div id="app">
    <Form @submitForm="onFormSubmit"/>
    <!-- <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <TotalBalance :total="totalBalance"/>
    <BudgetList :list="list" @deleteItem="onDeleteItem"/>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import BudgetList from '@/components/BudgetList';
import TotalBalance from '@/components/TotalBalance';
// import Form from '@/components/Form';
import Form from './components/Form.vue';

export default {
  name: 'app',
  components: {
    // HelloWorld
    BudgetList,
    TotalBalance,
    Form,
  },
  data: () => ({
    list: {
      1: {
        type: "INCOME",
        value: 100,
        comment: "Some comment",
        id: 1
      },
      2: {
        type: "OUTCOME",
        value: -50,
        comment: "Some outcome comment",
        id: 2
      },
    }
  }),
  computed: {
      totalBalance() {
        return Object.values(this.list).reduce((acc, item) => acc + item.value, 0);
    }
  },
  methods: {
    onDeleteItem(id) {
      this.$delete(this.list, id);
    },
    onFormSubmit(data) {
      console.log(data);
      const newObj = {
        ...data,
        id: String(Math.random())
      };

      this.$set(this.list, newObj.id, newObj);
    }
  }
}
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
