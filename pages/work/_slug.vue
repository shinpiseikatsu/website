<template>
  <div class="narrow">
    <h1 class="text-2xl mt-8">{{ work.fields.title }}</h1>
    <h1 class="text-2xl mb-4">{{ work.fields.titleEn }}</h1>
    <p class="mb-4">{{ work.fields.date.substr(0,10) }}</p>
    <img 
      :src="work.fields.images[0].fields.file.url" 
      :alt="work.fields.title"
      class="w-full display-block mx-auto"
    >
    <div class="content" v-html="$md.render(work.fields.content)"></div>
  </div>
</template>

<script>
import { createClient } from '~/plugins/contentful.js'
const client = createClient()
export default { 
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
</style>