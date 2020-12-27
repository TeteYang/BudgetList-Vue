<template>
    <div class="dinamicBtn">
      <el-button v-for="(btn, index) in btns"
        :key="index" :type="btn.type" :class="[btn.class]"
        round @click="activeTab(btn.class, index)"> {{ btn.name }}
      </el-button>
    </div>
</template>

<script>
export default {
  name: 'ButtonsTabs',
  data: () => ({
    btns: {
      1: {
        name: 'All',
        class: 'All',
      },
      2: {
        name: 'Income',
        class: 'Income',
        type: 'success',
      },
      3: {
        name: 'Outcome',
        class: 'Outcome',
        type: 'warning',
      },
    },
  }),
  methods: {
    activeTab(btnClass, index) {
      this.$emit('clickBtnTab', btnClass, index);
    },
  },
};
</script>

<style lang="scss">
  .dinamicBtn{
    margin: 0 0 15px 0;
}
</style>
