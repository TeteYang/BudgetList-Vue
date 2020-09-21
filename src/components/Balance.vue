<template>
<div class="total-balance" :value="total">
  <template v-if="total === 0">
    <div class="black">{{total}}</div>
  </template>
    <template v-if="total > 0">
    <div class="green">{{total}}</div>
  </template>
      <template v-if="total < 0">
    <div class="red">{{total}}</div>
  </template>
</div>
</template>

<script>
export default {
  name: 'Balance',
  data: () => ({
    value: 0,
  }),
  props: {
    total: {
      type: Number,
      default: 0,
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .total-balance{
    font-size: 26px;
    text-transform: uppercase;
    padding: 20px;
    text-align: center;
  }
  .black{
    color: black;
  }
  .green{
    color: green;
  }
  .red{
    color: red;
  }
</style>
