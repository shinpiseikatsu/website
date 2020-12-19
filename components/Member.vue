<template>
  <div class="member flex my-3">
    <div 
      class="avatar bg-cover bg-center rounded-full mr-2"
      :style=" 'background-image: url(' + member.fields.image.fields.file.url + ');' "
    ></div>
    <div class="text-sm text-justify">
      <p class="inline font-bold">{{ member.fields.name }}.</p>
      <p class="inline">{{ member.fields.bio }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ['member']
}
</script>

<style lang="stylus" scoped>
.member
  width 280px
  min-width 280px
  @media(max-width 599px)
    width 100%
.avatar
  width 3rem
  height 3rem
  min-width 3rem
  min-height 3rem
</style>