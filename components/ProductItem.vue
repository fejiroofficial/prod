<template>
  <div class="h-64 w-72 rounded-lg flex-grow sm:flex-grow-0 relative">
    <img
      :src="product.image"
      alt="product.name"
      class="object-fill h-64 w-full rounded-lg"
    />
    <div
      class="
        absolute
        text-center
        bg-black
        text-white
        rounded-b-lg
        inset-x-0
        bottom-0
        opacity-75
        py-2
      "
    >
      <div class="font-bold">{{ product.name }}</div>
      <div>{{ `$${product.price}` }}</div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    product: {
      type: Object,
      default: () => {},
      required: true,
    },
  },
}
</script>

<style lang="scss" scoped></style>
