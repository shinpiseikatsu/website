<template>
  <div class="narrow">
    <h1 class="text-2xl">{{ product.fields.title }}</h1>
    <h1 class="text-2xl mb-4" v-if="product.fields.titleEn">{{ product.fields.titleEn }}</h1>
    <p class="mb-4" v-if="product.fields.date">{{ product.fields.date.substr(0,10) }}</p>
    <no-ssr>
      <carousel
        :per-page="1"
        :loop="true"
        :pagination-padding="5"
        :autoplay-timeout="4000"
        :navigationEnabled="true"
      >
        <slide
          v-for="(img,index) in product.fields.images" 
          :key="index"
        >
          <img 
            :src="img.fields.file.url" 
            :alt="img.fields.file.name"
            class="w-full display-block mx-auto"
          >
        </slide>
      </carousel>
    </no-ssr>
    <div v-if="product.fields.content" class="content" v-html="$md.render(product.fields.content)"></div>
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