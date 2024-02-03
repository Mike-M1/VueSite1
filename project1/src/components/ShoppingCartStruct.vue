<template>
  <div>
    
      <div v-for="product in cartItems" :key="product.id">
        <img :src="product.imageUrl" />
        <div>
          <h3>{{ product.name }}</h3>
          <p>{{ product.price }}</p>
          <button @click="$emit('remove-from-cart', product.id)">Remove from Cart</button>
        </div>
      </div>
      <button>Checkout</button>
  </div>
</template>

<script>
export default {
  name: "ShoppingCartStruct",
  props: ["cartItems"],
};
</script>
