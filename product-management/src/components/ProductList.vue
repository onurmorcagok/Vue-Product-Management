<template>
  <div id="product-list">
    <h4 v-if="products.length == 0"><b>Product list empty ! </b></h4>
    <table v-else class="table table-lg">
      <thead class="thead-dark">
        <tr>
          <th>ID</th>
          <th>Product Name</th>
          <th>Category ID</th>
          <th>Quantity Per Unit</th>
          <th>Unit Price</th>
          <th>Units In Stock</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">
          <td v-if="updateID === product.id">
            <input
              v-model="product.id"
              type="text"
              class="form-control"
              id="product.id"
            />
          </td>
          <td v-else>
            {{ product.id }}
          </td>

          <td v-if="updateID === product.id">
            <input
              v-model="product.productName"
              type="text"
              class="form-control"
              id="product.name"
            />
          </td>
          <td v-else>
            {{ product.productName }}
          </td>

          <td v-if="updateID === product.id">
            <input
              v-model="product.categoryId"
              type="text"
              class="form-control"
              id="product.categoryId"
            />
          </td>
          <td v-else>
            {{ product.categoryId }}
          </td>

          <td v-if="updateID === product.id">
            <input
              v-model="product.quantityPerUnit"
              type="text"
              class="form-control"
              id="product.quantityPerUnit"
            />
          </td>
          <td v-else>
            {{ product.quantityPerUnit }}
          </td>

          <td v-if="updateID === product.id">
            <input
              v-model="product.unitPrice"
              type="text"
              class="form-control"
              id="product.unitPrice"
            />
          </td>
          <td v-else>
            {{ product.unitPrice }}
          </td>

          <td v-if="updateID === product.id">
            <input
              v-model="product.unitsInStock"
              type="text"
              class="form-control"
              id="product.unitsInStock"
            />
          </td>
          <td v-else>
            {{ product.unitsInStock }}
          </td>

          <td v-if="updateID !== product.id">
            <button
              @click="handleUpdate(product)"
              class="btn btn-sm btn-success"
            >
              Update
            </button>
            <button
              @click="handleDelete(product)"
              class="btn btn-sm btn-danger"
            >
              Delete
            </button>
          </td>

          <td v-else>
            <button @click="handleSave(product)" class="btn btn-sm btn-success">
              Save
            </button>
            <button @click="updateID = null" class="btn btn-sm btn-danger">
              Cancel
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "ProductList",
  data() {
    return {
      updateID: null,
    };
  },
  props: {
    products: {
      type: Array,
      required: true,
    },
  },
  methods: {
    handleDelete(product) {
      this.$emit("deleteProduct", product);
    },
    handleUpdate(product) {
      this.updateID = product.id;
    },
    handleSave(product) {
      this.$emit("updateProduct", product);
      this.updateID = null;
    },
  },
};
</script>

<style scoped>
#product-list {
  margin: 100px;
  text-align: center;
}

button {
  margin-right: 1em;
}

input {
  text-align: center;
}

h4 {
  margin-top: 1em;
}
</style>