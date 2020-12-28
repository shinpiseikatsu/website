<template>
  <div>
    <h1 class="text-2xl mt-8">{{ work.fields.title }}</h1>
    <h1 class="text-2xl mb-4" v-if="work.fields.titleEn">{{ work.fields.titleEn }}</h1>
    <p class="mb-4" v-if="work.fields.date">{{ work.fields.date.substr(0,10) }}</p>
      <carousel
        :per-page="1"
        :autoplay="true"
        :loop="true"
        :pagination-padding="5"
        :autoplay-timeout="4000"
        :navigationEnabled="true"
      >
        <slide
          v-for="(img,index) in work.fields.images" 
          :key="index"
        >
          <img 
            :src="img.fields.file.url" 
            :alt="img.fields.file.name"
            class="w-full display-block mx-auto"
          >
        </slide>
      </carousel>
    <div v-if="work.fields.content" class="content" v-html="$md.render(work.fields.content)"></div>
  </div>
</template>

<script>
import Carousel from 'vue-carousel/src/Carousel.vue'
import Slide from 'vue-carousel/src/Slide.vue'
import { createClient } from '~/plugins/contentful.js'
const client = createClient()
export default { 
  components: {
    Carousel,
    Slide
  },
  asyncData({params}) {
    return Promise.all([
      client.getEntries({
        'content_type': 'work',
        'fields.slug': params.slug
      })
    ]).then(([works]) => {
      return {
        work: works.items[0]
      }
    }).catch(console.error)
  }
}
</script>

<style lang="stylus">
.content
  p
    margin 1.5rem 0
    line-height 2rem
  ol
    list-style decimal inside
    font-family monospace, 'YuGothic', 'Yu Gothic'

.swiper-button-prev, .swiper-button-next
  color white
</style>