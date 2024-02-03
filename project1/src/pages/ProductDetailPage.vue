<template>
  <div>
    <div v-if="product">
      <div class="img-wrap">
        <img :src="product.imageUrl" />
      </div>
      <div class="product-details">
        <h1>{{ product.name }}</h1>
        <h3 class="price">{{ product.price }}</h3>

        <button class="add-to-cart" @click="addToCart" v-if="user">
          Add to Cart
        </button>

        <button @click="signIn" v-if="!user">Sign in to add to cart</button>
      </div>
    </div>
    <div v-if="!product">
      <NotFound />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import NotFound from "@/pages/NotFound.vue";
import {
  getAuth,
  sendSignInLinkToEmail,
  isSignInWithEmailLink,
  signInWithEmailLink,
} from "firebase/auth";

export default {
  name: "ProductDetailPage",
  data() {
    return {
      product: {},
    };
  },
  props: ["user"],
  components: {
    NotFound,
  },
  async created() {
    const auth = getAuth();
    if (isSignInWithEmailLink(auth, window.location.href)) {
      const email = window.localStorage.getItem("emailForSignIn");
      signInWithEmailLink(auth, email, window.location.href);
      alert("Signed in!");
      window.localStorage.removeItem("emailForSignIn");
    }

    const response = await axios.get(
      `/api/products/${this.$route.params.productId}`
    );
    const product = response.data;
    this.product = product;
  },
  methods: {
    async addToCart() {
      const response = await axios.post("/api/users/2345/cart", {
        id: this.$route.params.productId,
      });
      console.log(response.data);
      alert("Added to cart!");
    },
    signIn() {
      const email = prompt("Enter your email");
      const auth = getAuth();
      const actionCodeSettings = {
        url: `http://localhost:8081/products/${this.$route.params.productId}`,
        handleCodeInApp: true,
      };
      sendSignInLinkToEmail(auth, email, actionCodeSettings);
      alert(`Email sent to ${email}`);
      window.localStorage.setItem("emailForSignIn", email);
    },
  },
};
</script>
