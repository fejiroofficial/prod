<template>
  <div>
    <button
      v-for="(dp, i) in displayPages"
      :key="`pagination-page-${i}`"
      :class="{ 'bg-red-400 text-white': dp === currentPage }"
      class="h-10 w-10 mr-4 rounded focus:outline-none"
      @click="$emit('page-click', dp)"
    >
      {{ dp }}
    </button>
  </div>
</template>

<script>
export default {
  props: {
    currentPage: {
      type: Number,
      required: true,
      default: 1,
    },
    pages: {
      type: Number,
      required: true,
      default: 1,
    },
  },
  computed: {
    displayPages() {
      const displayPages = []
      for (let i = 0; i < this.pages; i++) {
        displayPages.push(i + 1)
      }
      return displayPages
    },
  },
}
</script>

<style lang="css" scoped></style>
