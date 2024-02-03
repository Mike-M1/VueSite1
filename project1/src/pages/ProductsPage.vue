<template>
  <div>
    <h1>All Products</h1>
    <ProductStruct :products="products" />
  </div>
</template>

<script>
import axios from "axios";
import ProductStruct from "@/components/ProductStruct.vue";

export default {
  name: "ProductsPage",
  components: {
    ProductStruct,
  },
  data() {
    return {
      products: [],
    };
  },
  async created() {
    const response = await axios.get("/api/products");
    const products = response.data;
    this.products = products;
  },
};
</script>
