<template>
  <div class="container mx-auto px-4">
    <h1 class="text-5xl text-gray-700 font-black text-center my-10">
      Products
    </h1>
    <div class="flex my-8 justify-center">
      <select v-model="selected" class="outline-none">
        <option disabled value="">Filter by categories:</option>
        <option v-for="category in categories" :key="`${category}`">
          {{ category }}
        </option>
      </select>
    </div>
    <div class="w-4/4 sm:justify-center flex flex-grow flex-wrap gap-4">
      <ProductItem
        v-for="product in products"
        :key="product.id"
        :product="product"
      />
    </div>
    <Pagination
      class="my-8 text-center"
      :current-page="currentPage"
      :pages="lastPage"
      @page-click="goPage"
    />
  </div>
</template>

<script>
import ProductItem from '@/components/ProductItem'
import Pagination from '@/components/Pagination'
export default {
  components: {
    ProductItem,
    Pagination,
  },
  data() {
    return {
      products: [],
      productsForComputation: [],
      allCategories: [],
      currentPage: 1,
      lastPage: 0,
      selected: '',
    }
  },
  async fetch() {
    const page = 1
    await this.getProducts(page)
  },
  computed: {
    categories() {
      const uniqueCategories = []
      this.productsForComputation.forEach((product) => {
        if (!uniqueCategories.includes(product.category)) {
          uniqueCategories.push(product.category)
        }
      })
      return uniqueCategories
    },
  },
  watch: {
    selected(val) {
      this.filterProducts(val)
    },
  },
  methods: {
    filterProducts(category) {
      const v = this.productsForComputation.filter(
        (product) => product.category === Number(category)
      )
      if (v.length) {
        this.products = v
      }
    },
    async getProducts(page) {
      const response = await this.$axios.$get(`/api/products?page=${page}`)
      this.products = response.data
      this.productsForComputation = response.data
      this.currentPage = response.current_page
      this.lastPage = response.last_page
      this.allCategories = this.products.map((item) => item.category)
    },
    goPage(pageNum) {
      if (pageNum <= this.lastPage) {
        this.currentPage = pageNum
        this.getProducts(pageNum)
      }
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
