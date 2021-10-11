<template>
  <section class="todo">
    <div class="row">
      <p class="title">Добавление товара</p>
      <select-input />
    </div>
    <div class="content row">
      <div class="sidebar-wrap"><sidebar-form :onCreate="onCreateProduct"></sidebar-form></div>
      <div class="products">
        <product v-for="item in products" :key="item.id" :data="item"></product>
      </div>
    </div>
  </section>
</template>

<script>
import Select from "./Select.vue";
import Form from "./Form.vue";
import Product from "./Product.vue";

export default {
  data: function () {
    return {
      products: [
        {
          description: "dsds",
          id: "1633937189602372875",
          image: "https://ru.vuejs.org/images/logo.png",
          name: "dsds",
          price: "131",
        },
        {
          description: "dsds",
          id: "1633937189602372876",
          image: "https://ru.vuejs.org/images/logo.png",
          name: "dsds",
          price: "131",
        },
        {
          description: "dsds",
          id: "1633937189602372877",
          image: "https://ru.vuejs.org/images/logo.png",
          name: "dsds",
          price: "131",
        },
        {
          description: "dsds",
          id: "1633937189602372878",
          image: "https://ru.vuejs.org/images/logo.png",
          name: "dsds",
          price: "131",
        },
        {
          description: "dsds",
          id: "1633937189602372879",
          image: "https://ru.vuejs.org/images/logo.png",
          name: "dsds",
          price: "131",
        },
        {
          description: "dsds",
          id: "1633937189602372880",
          image: "https://ru.vuejs.org/images/logo.png",
          name: "dsds",
          price: "131",
        },
        {
          description: "dsds",
          id: "1633937189602372881",
          image: "https://ru.vuejs.org/images/logo.png",
          name: "dsds",
          price: "131",
        },
        {
          description: "dsds",
          id: "1633937189602372882",
          image: "https://ru.vuejs.org/images/logo.png",
          name: "dsds",
          price: "131",
        },
        {
          description: "dsds",
          id: "1633937189602372883",
          image: "https://ru.vuejs.org/images/logo.png",
          name: "dsds",
          price: "131",
        },
      ],
    };
  },
  components: {
    "select-input": Select,
    "sidebar-form": Form,
    product: Product,
  },
  methods: {
    onCreateProduct(product) {
      return new Promise((resolve, reject) => {
        const resultProduct = {
          id:
            new Date().getTime().toString() +
            Math.floor(Math.random() * 1000000),
          name: product.name.value,
          description: product.description.value,
          image: product.productLink.value,
          price: product.price.value,
        };
        this.products.push(resultProduct);
        resolve();
      });
    },
  },
};
</script>

<style lang='less' scoped>
.todo {
  padding: 32px 32px 0px;
  width: 100%;
  margin: 0 auto;
  max-width: 1440px;
}
.row {
  justify-content: space-between;
}
.products {
  flex: 1;
  display: grid;
  grid-template-columns: repeat(auto-fit, 332px);
  grid-gap: 16px;
  height: 100%;
  max-height: calc(100vh - 67px);
  overflow: auto;
}
</style>