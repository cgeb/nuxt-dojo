<template>
  <div v-if="product">
    <Head>
      <Title> Nuxt Dojo | {{ product.title }} </Title>
      <Meta name="description" :content="product.description" />
    </Head>
    <ProductDetails :product="product" />
  </div>
</template>

<script setup lang="ts">
import { Product } from "./index.vue";

definePageMeta({
  layout: "products",
});

const { id } = useRoute().params;
const uri = `https://fakestoreapi.com/products/${id}`;

const { data: product } = await useFetch<Product>(uri);

if (!product.value) {
  throw createError({
    statusCode: 404,
    message: "Product not found",
    fatal: true,
  });
}
</script>

<style scoped>
h2 {
  margin-bottom: 20px;
  font-size: 36px;
}

p {
  margin: 20px 0;
}
</style>
