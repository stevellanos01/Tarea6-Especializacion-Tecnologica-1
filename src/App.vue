<template>
  <div class="container">
    <div class="row">
      <div class="col-md-12">
        <h1>Productos</h1>
      </div>
    </div>
    <div class="row">
      <div class="col-md-12">
        <product-form @add-product="addProduct" />
        <product-table
          :products="products"
          @delete-product="deleteProduct"
          @update-product="updateProduct"
        />
      </div>
    </div>
  </div>
</template>

<script>
import ProductForm from "./components/ProductForm.vue";
import ProductTable from "./components/ProductTable.vue";

export default {
  name: "app",
  components: {
    ProductTable,
    ProductForm,
  },

  data() {
    return {
      products: [],
    };
  },
  methods: {
    addProduct(product) {
      this.products = [...this.products, product];
    },
    deleteProduct(index) {
      this.products.splice(index, 1);
    },
    updateProduct(editIndex, editProduct) {
      this.products = this.products.map((product, index) =>
        index === editIndex ? editProduct : product
      );
    },
  },
};
</script>

<style scoded>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
