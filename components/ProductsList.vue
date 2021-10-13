<template>
  <section class="todo">
    <div class="row">
      <p class="title">Добавление товара</p>
      <select-input :callback="onChangeSort" />
    </div>
    <div class="content row">
      <div class="sidebar-wrap">
        <sidebar-form :onCreate="onCreateProduct"></sidebar-form>
      </div>
      <div class="products-wrap">
        <div v-if="loading" class="loader-wrap">
          <div class="lds-ring">
            <div></div>
            <div></div>
            <div></div>
            <div></div>
          </div>
        </div>
        <transition-group
          v-else-if="products.length"
          name="products-complete"
          tag="div"
          class="products"
        >
          <product
            :onDelete="onDeleteProduct"
            v-for="item in products"
            :key="item.id"
            :data="item"
          ></product>
        </transition-group>
        <p v-else class="no-data">Не найдено товаров</p>
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
      products: [],
      loading: true,
    };
  },
  components: {
    "select-input": Select,
    "sidebar-form": Form,
    product: Product,
  },
  mounted: function () {
    try {
      this.products = JSON.parse(localStorage.getItem("products")) || [];
      this.loading = false;
    } catch (error) {
      this.products = [];
      this.loading = false;
    }
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
        localStorage.setItem("products", JSON.stringify(this.products));
        resolve();
      });
    },
    onDeleteProduct(id) {
      this.products = this.products.filter((product) => product.id !== id);
      localStorage.setItem("products", JSON.stringify(this.products));
    },
    onChangeSort(sortValue) {
      const sortFuncs = {
        name: (a, b) => (a.name > b.name ? 1 : -1),
        maxPrice: (a, b) => Number(b.price) - Number(a.price),
        minPrice: (a, b) => Number(a.price) - Number(b.price),
      };
      this.products = this.products.sort(sortFuncs[sortValue]);
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

  @media (max-width: 768px) {
    padding: 16px;
  }
}
.row {
  justify-content: space-between;
  margin-bottom: 16px;

  @media (max-width: 768px) {
    flex-direction: column;
  }
}
.products-wrap {
  flex: 1;
  position: relative;
}
.products {
  flex: 1;
  display: grid;
  grid-template-columns: repeat(auto-fit, 332px);
  grid-gap: 16px;
  height: 100%;
  max-height: calc(100vh - 100px);
  overflow-y: auto;
  overflow-x: hidden;
  justify-content: center;

  @media (max-width: 768px) {
    margin-top: 16px;
    grid-template-columns: repeat(auto-fit, 100%);
    overflow: hidden;
  }
}
.no-data {
  flex: 1;
  text-align: center;
}
.products-complete-enter,
.products-complete-leave-to {
  opacity: 0;
}
.products-complete-leave-active {
  position: absolute;
}
.loader-wrap {
  width: 100%;
  height: 100%;
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>