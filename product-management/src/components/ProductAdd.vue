<template>
  <div id="product-add">
    <form @submit.prevent="handleAdd">
      <div class="form-group">
        <label for="categoryId">Category ID</label>
        <input
          v-model="products.categoryId"
          type="text"
          class="form-control"
          id="categoryId"
        />
      </div>

      <div class="form-group">
        <label for="productName">Product Name</label>
        <input
          v-model="products.productName"
          type="text"
          class="form-control"
          id="productName"
        />
      </div>

      <div class="form-group">
        <label for="quantityPerUnit">Quantity Per Unit</label>
        <input
          v-model="products.quantityPerUnit"
          type="text"
          class="form-control"
          id="quantityPerUnit"
        />
      </div>

      <div class="form-group">
        <label for="unitPrice">Unit Price</label>
        <input
          v-model="products.unitPrice"
          type="text"
          class="form-control"
          id="unitPrice"
        />
      </div>

      <div class="form-group">
        <label for="unitsInStock">Units In Stock</label>
        <input
          v-model="products.unitsInStock"
          type="text"
          class="form-control"
          id="unitsInStock"
        />
      </div>
      <button type="submit" class="btn btn-sm btn-success">Add Product</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "ProductAdd",
  data() {
    return {
      products: {
        id: "",
        categoryId: "",
        productName: "",
        quantityPerUnit: "",
        unitPrice: "",
        unitsInStock: "",
      },
    };
  },
  methods: {
    handleAdd() {
      this.$emit("addProduct", this.products);
    },
  },
};
</script>

<style scoped>
#product-add {
  margin: 100px;
  margin-top: 50px;
}
</style>