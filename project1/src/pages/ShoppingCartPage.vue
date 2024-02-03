<template>
  <div>
    <h1>Shopping Cart Page</h1>
    <div v-if="cartItems.length > 0">
      <ShoppingCartStruct :cartItems="cartItems" @remove-from-cart="removeFromCart($event)" />
    </div>
    <div v-if="cartItems.length === 0">
      <h1>Your cart is empty</h1>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import ShoppingCartStruct from "@/components/ShoppingCartStruct.vue";

export default {
  name: "ShoppingCartPage",
  data() {
    return {
      cartItems: [],
    };
  },
  components: {
    ShoppingCartStruct,
  },
  async created() {
    const response = await axios.get("/api/users/2345/cart");
    const cartItems = response.data;
    this.cartItems = cartItems;
  },
  methods: {
    async removeFromCart(productId){
      const response = await axios.delete(`/api/users/2345/cart/${productId}`);
      const updatedCart = response.data;
      this.cartItems = updatedCart;
      }
    }
  
};
</script>
