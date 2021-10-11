<template>
  <button
    v-on:click="isFormValid ? callback() : () => {}"
    :class="{ 'submit-btn': true, disabled: !isFormValid }"
  >
    {{ text }}
  </button>
</template>

<script>
export default {
  props: {
    text: String,
    isFormValid: {
      type: Boolean,
      default: false,
    },
    callback: Function,
  },
};
</script>

<style lang="less" scoped>
.submit-btn {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px 0px;
  background: #7bae73;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  color: #fff;

  &.disabled {
    background: #eeeeee;
    color: #b4b4b4;
    font-weight: 600;
    font-size: 12px;
    cursor: not-allowed;
  }
}
</style>