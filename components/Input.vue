<template>
  <div class="input-wrapper">
    <p v-bind:class="{ 'input-name': true, required: isRequired }">
      {{ name }}
    </p>
    <textarea
      v-on:input="onChange"
      v-model="val.value"
      v-if="isMulti"
      class="input multi"
      :type="type"
      :placeholder="placeholder"
    />
    <input
      v-on:input="onChange"
      v-model="val.value"
      v-else
      :type="type"
      :class="{ input: true, error: val.isError }"
      :placeholder="placeholder"
    />
    <p :class="{ 'input-error': true, show: val.isError }">
      Поле является обязательным
    </p>
  </div>
</template>

<script>
export default {
  props: {
    placeholder: String,
    name: String,
    type: String,
    field: String,
    val: Object,
    isRequired: {
      type: Boolean,
      default: false,
    },
    isMulti: {
      type: Boolean,
      default: false,
    },
    callback: {
      type: Function,
      default: () => {},
    },
  },
  methods: {
    onChange(e) {
      const { value } = e.target;
      this.callback(this.field, value);
    },
  },
};
</script>

<style lang="less" scoped>
.input-wrapper {
  & * {
    &:not(:last-child) {
      margin-bottom: 4px;
    }
  }
}
.input {
  background: #fffefb;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  font-size: 12px;
  color: #3f3f3f;
  width: 100%;

  &.multi {
    min-height: 108px;
  }

  &.error {
    border: 1px solid #ff8484;
  }
}
.input-name {
  font-size: 10px;
  color: #49485e;
  display: flex;

  &.required {
    &:after {
      content: "";
      display: block;
      min-width: 4px;
      min-height: 4px;
      width: 4px;
      height: 4px;
      background: #ff8484;
      border-radius: 50%;
    }
  }
}
.input-error {
  font-size: 8px;
  color: #ff8484;
  opacity: 0;

  &.show {
    opacity: 1;
  }
}
</style>