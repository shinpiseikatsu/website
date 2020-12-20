<template>
  <div 
    class="item overflow-hidden m-1 cursor-pointer"
    @click="$router.push('/work/' + work.fields.slug)"
  >
      <div 
        :style=" 'background-image: url(' + work.fields.images[0].fields.file.url + '); height: 180px;'" 
        :alt="work.fields.title"
        class="w-full bg-cover bg-center bg-no-repeat"
      ></div>
    </div>
</template>

<script>
export default {
  props: ['work']
}
</script>

<style lang="stylus" scoped>
.item
  width 280px
  min-width 280px
  transition all .5s
  @media(max-width 599px)
    width 100%
</style>