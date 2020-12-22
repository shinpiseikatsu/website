<template>
  <div class="narrow">
    <h1 class="text-2xl mt-8">{{ work.fields.title }}</h1>
    <h1 class="text-2xl mb-4">{{ work.fields.titleEn }}</h1>
    <p class="mb-4">{{ work.fields.date.substr(0,10) }}</p>
    <swiper ref="mySwiper" :options="swiperOptions">
      <swiper-slide
        v-for="(img,index) in work.fields.images" 
        :key="index"
      >
        <img 
          :src="img.fields.file.url" 
          :alt="img.fields.file.name"
          class="w-full display-block mx-auto"
        >
      </swiper-slide>
      <div class="swiper-button-next" slot="button-next"></div>
      <div class="swiper-button-prev" slot="button-prev"></div>
    </swiper>
    <div class="content" v-html="$md.render(work.fields.content)"></div>
  </div>
</template>

<script>
import { createClient } from '~/plugins/contentful.js'
const client = createClient()
export default { 
  data() {
    return {
      swiperOptions: {
        pagination: {
          el: '.swiper-pagination'
        },
        navigation: {
          nextEl: '.swiper-button-next',
          prevEl: '.swiper-button-prev'
        }
      }
    }
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
  li
    list-style unset

.swiper-button-prev, .swiper-button-next
  color white
</style>