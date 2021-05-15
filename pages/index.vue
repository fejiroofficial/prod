<template>
  <div class="container justify-center mx-auto px-4">
    <h1 class="text-center">Products</h1>
    <div class="w-4/4 sm:justify-center flex flex-grow flex-wrap gap-4">
      <ProductItem
        v-for="product in products"
        :key="product.id"
        :product="product"
      />
    </div>
  </div>
</template>

<script>
import ProductItem from '@/components/ProductItem'
export default {
  components: {
    ProductItem,
  },
  data() {
    return {
      products: [],
    }
  },
  async fetch() {
    const page = 1
    await this.getProducts(page)
  },
  methods: {
    async getProducts(page) {
      const response = await this.$axios.$get(`/api/products?page=${page}`)
      this.products = response.data
    },
  },
}
</script>

<style>
.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}
</style>
