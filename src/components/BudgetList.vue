/* eslint-disable no-restricted-globals */
/* eslint-disable no-restricted-globals */
/* eslint-disable no-alert */
<template>
  <div class='budget-list-wrap'>
    <template v-if="isEmpty">
    <ElCard :header="header">
      <BudgetListItem :list="list" @deleteItem="deleteItemList"
      :notView="notView" :typeTbs="typeTbs"/>
    </ElCard>
    </template>
    <ElAlert v-else type="info" :title="emptyTitle"  />
    {{ text }}
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
    text: {
      type: String,
    },
    notView: {
      type: Boolean,
    },
    typeTbs: {
      type: String,
    },
  },
  data: () => ({
    header: 'Budget List',
    emptyTitle: 'Empty list',
  }),
  computed: {
    isEmpty() {
      return Boolean(Object.keys(this.list).length);
    },
  },
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
