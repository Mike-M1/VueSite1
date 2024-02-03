<template>
       <div class="grid-wrap">
        <div v-for="product in products" :key="product.id">
            <img :src="product.imageUrl" />
            <h3>{{ product.name }}</h3>
            <p>{{ product.price }}</p>
            <router-link :to="'/products/' + product.id">
            <button>View Details</button>
            </router-link>
        </div>
    </div>
</template>

<script>

export default {
    name: "ProductStruct",
    props: ["products"],
}

</script>