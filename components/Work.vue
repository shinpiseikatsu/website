<template>
  <nuxt-link :to=" '/work/' + work.fields.slug ">
    <img v-if="work.fields.images.length > 0 && work.fields.images[0].fields.file.contentType.split('/')[0] == 'image'"
      :src="work.fields.images[0].fields.file.url" 
      :alt="work.fields.title"
      class="item my-1"
    />
    <video
      v-else
      :src="work.fields.images[0].fields.file.url"
      :alt="work.fields.title"
      :ref="'video' + work.sys.id"
      @mouseover="videoController(true, work.sys.id)"
      @mouseleave="videoController(false, work.sys.id)"
      class="item my-1"
      playsinline
    ></video>
  </nuxt-link>
</template>

<script>
export default {
  props: ['work'],
  methods: {
    videoController(isHovering, index) {
      if (isHovering == true) {
        this.$refs['video' + index].play()
      }
      else if (isHovering == false) {
        this.$refs['video' + index].pause()
      }
    }
  }
}
</script>

<style lang="stylus" scoped>
.item
  object-fit cover
  width 100%
  transition .2s
</style>