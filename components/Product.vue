<template>
  <nuxt-link :to=" '/products/' + product.fields.slug ">
    <img v-if="product.fields.images.length > 0"
      :src="product.fields.images[0].fields.file.url" 
      :alt="product.fields.title"
      class="item my-1"
    />
  </nuxt-link>
</template>

<script>
export default {
  props: ['product']
}
</script>

<style lang="stylus" scoped>
.item
  object-fit cover
  width 100%
  transition .2s
</style>