<template>
    <div>
        <router-link to="/products">
            <img :src="jordan" />
        </router-link>
        <router-link to="/cart" >
        <button>Shopping Cart </button>
        </router-link>
    </div>
</template>

<script>
import jordan from "@/assets/shoeimages/jordan.png";

export default {
    name: "NavBar",
    data(){
        return {
            jordan
        }
    }
};
</script>