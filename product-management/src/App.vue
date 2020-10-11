<template>
  <div id="app">
    <h1 class="bg-danger">Product List App</h1>
    <ProductAdd @addProduct="addProduct"></ProductAdd>
    <ProductList
      :products="products"
      @deleteProduct="deleteProduct"
      @updateProduct="updateProduct"
    ></ProductList>
  </div>
</template>

<script>
import ProductList from "./components/ProductList";
import ProductAdd from "./components/ProductAdd";
export default {
  name: "App",
  components: {
    ProductList,
    ProductAdd,
  },
  data() {
    return {
      products: [
        {
          id: 1,
          categoryId: 1,
          productName: "iPhone 6S",
          quantityPerUnit: "Apple Mobile Phone",
          unitPrice: 15000,
          unitsInStock: 10,
        },
        {
          id: 2,
          categoryId: 1,
          productName: "Samsung Galaxy Tab E",
          quantityPerUnit: "Samsung Tablet",
          unitPrice: 4500,
          unitsInStock: 5,
        },
        {
          id: 3,
          categoryId: 2,
          productName: "Xiaomi Mi Band 5",
          quantityPerUnit: "Xiaomi Watch",
          unitPrice: 1250,
          unitsInStock: 20,
        },
      ],
    };
  },
  methods: {
    deleteProduct(product) {
      this.products = this.products.filter(
        (productToFilter) => productToFilter.id !== product.id
      );
    },
    updateProduct() {},
    addProduct(product) {
      const newProduct = { ...product };
      this.products = [...this.products, newProduct];
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
}

h1 {
  margin-bottom: 0;
  text-align:center;
  padding: 1em;
  color: #fff;
}
</style>
