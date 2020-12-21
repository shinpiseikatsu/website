<template>
  <img 
    :src="work.fields.images[0].fields.file.url" 
    :alt="work.fields.title"
    class="item m-1"
  />
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