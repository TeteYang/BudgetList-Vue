<template>
  <div id="app">
    <template>
      <h1>{{text}}</h1>
    </template>
    <Balance :total="totalBalance" />
    <ButtonsTabs @clickBtnTab="clickBtnTab" />
    <BudgetList
    :list="list"
    :text="hello"
    :typeTbs="typeTbs"
    :alertVisible="alertVisible"
    :visibleList="visibleList"
     />
    <Form @submitForm="onSubmit"  />
  <el-dialog
        title="Attention!"
        :visible.sync="centerDialogVisible"
        width="30%"
        center>
    <span>Enter a negative value</span>
    <span slot="footer" class="dialog-footer">
      <el-button type="primary" @click="centerDialogVisible = false">Confirm</el-button>
    </span>
  </el-dialog>
  </div>
</template>

<script>
import Balance from './components/Balance.vue';
import ButtonsTabs from './components/ButtonsTabs.vue';
import Form from './components/Form.vue';
import BudgetList from './components/BudgetList.vue';

export default {
  name: 'App',
  components: {
    Balance,
    Form,
    BudgetList,
    ButtonsTabs,
  },
  data: () => ({
    text: 'Budget',
    typeTbs: '',
    visibleList: true,
    centerDialogVisible: false,
    alertVisible: false,
    list: {
      1: {
        type: 'Income',
        value: 100,
        comment: 'Some income comment',
        id: 1,
        styled: 'color: green el-icon-top',
        isNotActive: false,
      },
      2: {
        type: 'Outcome',
        value: -50,
        comment: 'Some outcome comment',
        id: 2,
        styled: 'color: red el-icon-bottom',
        isNotActive: false,
      },
    },
    hello: 'Hello',
  }),
  computed: {
    totalBalance() {
      const balance = Object.values(this.list).reduce((acc, item) => acc + item.value, 0);
      return balance;
    },
  },
  methods: {
    // eslint-disable-next-line consistent-return
    onSubmit(data) {
      const newObj = {
        ...data,
        id: String(Math.random()),
      };
      if (newObj.type === 'Income') {
        newObj.styled = 'color: green el-icon-top';
      } else {
        newObj.styled = 'color: red el-icon-bottom';
      }
      if (newObj.value > 0 && newObj.type === 'Outcome') {
        this.centerDialogVisible = !this.centerDialogVisible;
        return this.list;
      }
      this.$set(this.list, newObj.id, newObj);
    },
    clickBtnTab(btnClass) {
      Object.values(this.list)
        // eslint-disable-next-line consistent-return
        .forEach((item) => {
          if (btnClass === item.type) {
            this.typeTbs = btnClass;
            this.visibleList = item.isNotActive;
          } else if (btnClass === 'All') {
            this.typeTbs = btnClass;
          }
          Object.values(this.list);
          if (Object.keys(this.list).length <= 1 && btnClass === 'Income') {
            this.alertVisible = true;
          } else if (Object.keys(this.list).length <= 1 && btnClass === 'Outcome') {
            this.alertVisible = true;
          }
          return this.alertVisible;
        });
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
