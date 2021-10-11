<template>
  <div class="wrap">
    <button v-on:click="onSelect" class="select-button row">
      {{ value || "По умолчанию" }}
    </button>
    <div v-if="isOpen" class="select-options-list">
      <p
        v-on:click="onClickOption($event, item)"
        v-for="item in sortOptions"
        :key="item.value"
      >
        {{ item.text }}
      </p>
    </div>
  </div>
</template>

<script>
import { sortOptions } from "../utils/contants";
export default {
  data: function () {
    return {
      isOpen: false,
      value: "По умолчанию",
      sortOptions,
    };
  },
  methods: {
    onClickOption: function (e, item) {
      this.isOpen = false;
      this.value = item.text || "";
    },
    onSelect: function (e) {
      this.isOpen = !this.isOpen;
    },
  },
};
</script>

<style lang="less" scoped>
.wrap {
  position: relative;
}
.select-button {
  padding: 10px 16px;
  background: #fffefb;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  font-weight: 400;
  font-size: 12px;
  line-height: 15px;
  color: #b4b4b4;
  border: none;
  width: 100%;

  &::after {
    content: "";
    background-repeat: no-repeat;
    background-size: contain;
    background-position: center;
    background-image: url("~/assets/images/arrow.png");
    width: 15px;
    height: 10px;
  }
}

.select-options-list {
  position: absolute;
  z-index: 1;
  top: 35px;
  background: #fffefb;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  padding: 10px 16px;
  width: 100%;
  & * {
    cursor: pointer;
    font-size: 12px;

    &:not(:last-child) {
      margin-bottom: 10px;
    }
  }
}
</style>