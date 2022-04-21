<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newProduct: {},
      errors: [],
    };
  },
  created: function () {},
  methods: {
    createProduct: function () {
      axios
        .post("/products", this.newProduct)
        .then((response) => {
          console.log("products create", response);
          this.$router.push("/products");
        })
        .catch((error) => {
          console.log("products create error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="products-new">
    <h1>New Product</h1>
    <form v-on:submit.prevent="createProduct()">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      Name:
      <input type="text" v-model="newProduct.name" />
      Price:
      <input type="text" v-model="newProduct.price" />
      Description:
      <input type="text" v-model="newProduct.description" />
      Image:
      <!-- <input type="text" v-model="newProduct.image_url" /> -->
      <input type="submit" value="Create Product" />
    </form>
  </div>
</template>

<style></style>
