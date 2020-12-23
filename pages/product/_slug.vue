<template>
  <div>
    <h1 class="text-2xl mt-8">{{ product.fields.title }}</h1>
    <h1 class="text-2xl mb-4" v-if="product.fields.titleEn">{{ product.fields.titleEn }}</h1>
    <p class="mb-4" v-if="product.fields.date">{{ product.fields.date.substr(0,10) }}</p>
    <swiper ref="mySwiper" :options="swiperOptions" v-if="product.fields.images.length > 0">
      <swiper-slide
        v-for="(img,index) in product.fields.images" 
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
    <div v-if="product.fields.content" class="content" v-html="$md.render(product.fields.content)"></div>
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
        'content_type': 'product',
        'fields.slug': params.slug
      })
    ]).then(([products]) => {
      return {
        product: products.items[0]
      }
    }).catch(console.error)
  }
}
</script>