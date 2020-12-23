<template>
  <nuxt-link :to=" '/work/' + work.fields.slug ">
    <img v-if="work.fields.images.length > 0"
      :src="work.fields.images[0].fields.file.url" 
      :alt="work.fields.title"
      class="item m-1"
    />
  </nuxt-link>
</template>

<script>
export default {
  props: ['work']
}
</script>

<style lang="stylus" scoped>
.item
  object-fit cover
  width 100%
  transition .2s
</style>