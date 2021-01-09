<template>
  <div class="narrow">
    <h1 class="text-2xl">{{ work.fields.title }}</h1>
    <h1 class="text-2xl mb-4" v-if="work.fields.titleEn">{{ work.fields.titleEn }}</h1>
    <p class="mb-4" v-if="work.fields.date">{{ work.fields.date.substr(0,10) }}</p>
    <no-ssr>
      <carousel
        :per-page="1"
        :loop="true"
        :pagination-padding="5"
        :navigationEnabled="true"
      >
        <slide
          v-for="(img,index) in work.fields.images" 
          :key="index"
        >
          <div 
            v-if="img.fields.file.contentType.split('/')[0] == 'image'"
            :style=" 'background: url(' + img.fields.file.url + ')' " 
            class="photo"
          ></div>
          <video
            v-else
            :src="img.fields.file.url"
            :alt="work.fields.title"
            class="w-full display-block mx-auto"
            autoplay
            muted
            controls
            playsinline
          ></video>
        </slide>
      </carousel>
    </no-ssr>
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
.VueCarousel-navigation-button
  position absolute
  top 45%
  -webkit-box-sizing border-box
  box-sizing border-box
  color #000
  text-decoration none
  -webkit-appearance none
  -moz-appearance none
  appearance none
  border none
  background-color transparent
  padding 0
  cursor pointer
  outline none
  @media(max-width 900px)
    display none
.VueCarousel-navigation-prev
  left 0
  -webkit-transform translateY(-50%) translateX(-100%)
  transform translateY(-50%) translateX(-100%)
  font-family "system"
.VueCarousel-navigation-next
  right 0
  -webkit-transform translateY(-50%) translateX(100%)
  transform translateY(-50%) translateX(100%)
  font-family "system"
.VueCarousel-pagination
  width 100%
  text-align center
.VueCarousel-dot
  display inline-block
  cursor pointer
  -webkit-appearance none
  -moz-appearance none
  appearance none
  border none
  background-clip content-box
  -webkit-box-sizing content-box
  box-sizing content-box
  padding 0
  border-radius 100%
  outline none
button:focus
  border none!important
  outline none!important
.photo
  width 100%
  height 400px
  background-repeat no-repeat!important
  background-size contain!important
  background-position center!important
  @media (max-width 700px)
    height 250px
</style>