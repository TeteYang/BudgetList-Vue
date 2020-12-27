/* eslint-disable consistent-return */
/* eslint-disable consistent-return */
<template>
  <div>
    <div v-for="(item, index) in list" :key="index"
    v-show="visibleList || typeTbs == 'All' || typeTbs == item.type" >
      <i class="list-item" :class="[item.styled]">
        <span class="budget-comment">
          {{item.comment}}
        </span>
        <span class="budget-value">
          {{item.value}}
        </span>
          <el-button type="danger" size="mini"
          @click="onDeleteItem(item.id)">
            Delete
          </el-button>
      </i>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BudgetListItem',
  data: () => ({
  }),
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
    visibleList: {
      type: Boolean,
    },
  },
  methods: {
    // eslint-disable-next-line consistent-return
    onDeleteItem(id) {
      this.$emit('deleteItem', id);
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
