<template>
  <div class="narrow">
    <h1 class="text-2xl mt-8">{{ work.fields.title }}</h1>
    <h1 class="text-2xl mb-4">{{ work.fields.titleEn }}</h1>
    <p class="mb-4">{{ work.fields.date.substr(0,10) }}</p>
    <swiper :options="swiperOption">
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
      <div
        slot="pagination"
        class="swiper-pagination"
      />
      <div
        slot="button-prev"
        class="swiper-button-prev"
      />
      <div
        slot="button-next"
        class="swiper-button-next"
      />
    </swiper>
    <div class="content" v-html="$md.render(work.fields.content)"></div>
  </div>
</template>

<script>
import { Swiper, SwiperSlide, directive } from 'vue-awesome-swiper'
import 'swiper/swiper-bundle.css'
import { createClient } from '~/plugins/contentful.js'
const client = createClient()
export default { 
  data() {
    return {
      swiperOption: {
        speed: 1000, //スライドの切り替わりスピード
        spaceBetween: 30, //各スライドの余白
        centeredSlides: true, //スライダーを真ん中に
        loop: true, //無限ループ
        autoplay: { //スライドの自動切り替え
          delay: 5000, //スライドの自動切り替えの秒数
          disableOnInteraction: false //何らかのアクション後の自動切り替えを再開
        },
        navigation: {
          nextEl: '.swiper-button-next',
          prevEl: '.swiper-button-prev'
        }
      }
    }
  },
  components: {
    Swiper,
    SwiperSlide
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
</style>