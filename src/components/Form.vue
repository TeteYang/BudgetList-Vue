<template>
  <ElCard class="card-form">
    <ElForm :model="formData" ref="addItemForm" :rules="rules">
      <ElFormItem label="Type" prop="type">
        <ElSelect v-model="formData.type" placeholder="Choose type">
          <ElOption label="Income" value="Income"/>
          <ElOption label="Outcome" value="Outcome"/>
        </ElSelect>
      </ElFormItem>
      <ElFormItem label="Comments" prop="comment">
          <ElInput v-model="formData.comment"/>
      </ElFormItem>
      <ElFormItem label="Value" prop="value">
          <ElInput v-model.number="formData.value"/>
      </ElFormItem>
      <ElButton @click="onSubmit" type="primary">
        Submit
      </ElButton>
    </ElForm>
  </ElCard>
</template>

<script>
export default {
  name: 'Form',
  props: {
    centerDialogVisible: {
      type: Boolean,
    },
  },
  data: () => ({
    formData: {
      type: 'Income',
      comment: '',
      value: 0,
      styled: '',
    },
    rules: {
      type: [
        {
          required: true,
          message: 'Please select type',
          trigger: 'blur',
        },
      ],
      comment: [
        {
          required: true,
          message: 'Please input comment',
          trigger: 'blur',
        },
      ],
      value: [
        {
          required: true,
          message: 'Please input value',
          trigger: 'change',
        },
      ],
    },
  }),
  methods: {
    // eslint-disable-next-line consistent-return
    onSubmit() {
      const objZeroValue = {
        message: 'The value must not be 0',
        trigger: 'change',
      };
      const objStrValue = {
        type: 'number',
        message: 'The value should not be a string',
        trigger: 'change',
      };
      if (this.formData.value === 0) {
        this.$set(this.rules.value, 1, objZeroValue);
      } else if (typeof this.formData.value === 'string') {
        this.$set(this.rules.value, 2, objStrValue);
      } else {
        this.rules.value.splice(1, 1);
        this.rules.value.splice(1, 2);
      }
      this.$refs.addItemForm.validate((valid) => {
        // console.log(valid); // проврка на заполнение формы
        if (valid) {
          this.$emit('submitForm', { ...this.formData });
          this.$refs.addItemForm.resetFields(); // очистка формы
        }
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .card-form{
        width: 80vw;
        margin: 10px auto;
  }
</style>
