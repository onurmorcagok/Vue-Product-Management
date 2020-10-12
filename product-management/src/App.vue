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
      products: [],
    };
  },
  created() {
    this.getProducts();
  },
  methods: {
    async getProducts() {
      const result = await fetch('http://localhost:3000/products');
      const data = await result.json();
      this.products = data;
    },
    async deleteProduct(product) {
      await fetch('http://localhost:3000/products/' + product.id, {
        method: "DELETE",
      });
      this.products = this.products.filter(
        (productToFilter) => productToFilter.id !== product.id
      );
    },
    async updateProduct(product) {
      const result = await fetch('http://localhost:3000/products/' + product.id , {
        method: "PUT",
        body: JSON.stringify(product),
        headers: { "Content-Type": "application/json" },
      });

      const updatedProduct = await result.json();

      this.products = this.products.map(product => product.id === updatedProduct ? updatedProduct : product);
    },
    async addProduct(product) {
      const result = await fetch('http://localhost:3000/products', {
        method: "POST",
        body: JSON.stringify(product),
        headers: { "Content-Type": "application/json" },
      });
      const newProduct = await result.json();
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
  text-align: center;
  padding: 1em;
  color: #fff;
}
</style>
