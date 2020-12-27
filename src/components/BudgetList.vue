/* eslint-disable no-restricted-globals */
/* eslint-disable no-restricted-globals */
/* eslint-disable no-alert */
<template>
  <div class='budget-list-wrap'>
    <template>
    <ElCard :header="header">
      <BudgetListItem
      :list="list"
      @deleteItem="deleteItemList"
      :typeTbs="typeTbs"
      :visibleList="visibleList"
      />
      <ElAlert type="info" :title="emptyTitle" v-show="alertVisible"/>
    </ElCard>
    </template>
  </div>
</template>

<script>
import BudgetListItem from './BudgetListItem.vue';

export default {
  components: {
    BudgetListItem,
  },
  name: 'BudgetList',
  props: {
    list: {
      type: Object,
      default: () => ({}),
    },
    typeTbs: {
      type: String,
    },
    alertVisible: {
      type: Boolean,
    },
    visibleList: {
      type: Boolean,
    },
  },
  data: () => ({
    header: 'Budget List',
    emptyTitle: 'Empty list',
  }),
  methods: {
    // eslint-disable-next-line consistent-return
    deleteItemList(id) {
      this.$delete(this.list, id);
    },
  },
};
</script>

<style scoped lang="scss">
  .budget-list-wrap{
    width: 80vw;
    margin: 0 auto;
  }
</style>
