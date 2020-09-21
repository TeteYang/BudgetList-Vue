/* eslint-disable consistent-return */
/* eslint-disable consistent-return */
<template>
  <div>
    <div v-for="(item, index) in list" :key="index"
    v-show="(typeTbs == item.type) == notView || typeTbs == Object.keys(list).length || !notView">
      <i class="list-item" :class="item.styled" v-if="isType(item)">
        <span class="budget-comment">
          {{item.comment}}
        </span>
        <span class="budget-value">
          {{item.value}}
        </span>
          <el-button type="danger" size="mini"
          @click="onDeleteItem(item.id, item.type)">
            Delete
          </el-button>
      </i>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BudgetListItem',
  props: {
    list: {
      type: Object,
      default: () => ({}),
    },
    notView: {
      type: Boolean,
    },
    typeTbs: {
      type: String,
    },
  },
  data: () => ({
  }),
  methods: {
    // eslint-disable-next-line consistent-return
    onDeleteItem(id) {
      this.$emit('deleteItem', id);
    },
    // eslint-disable-next-line consistent-return
    isType(item) {
      if (item.type === 'Income') {
        return item;
      // eslint-disable-next-line no-else-return
      } else if (item.type === 'Outcome') {
        return item;
      }
    },
  },
};
</script>

<style scoped lang="scss">
  .list-item{
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 10px 15px;
  }
  .budget-value{
    font-weight: bold;
    margin-left: auto;
    margin-right: 20px;
  }
  .green{
    color: green;
  }
  .red{
    color: red;
  }
</style>
