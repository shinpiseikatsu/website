<template>
  <div>
    <h2 class="text-3xl my-2">新皮生活</h2>
    <div 
      v-html="$md.render(texts.fields.aboutJp)"
      class="about mb-16"
    ></div>
    <h2 class="text-3xl my-2">Shinpiseikatsu</h2>
    <div 
      v-html="$md.render(texts.fields.aboutEn)"
      class="about"
    ></div>
  </div>
</template>

<script>
import { createClient } from '~/plugins/contentful.js'
const client = createClient()
export default { 
  asyncData() {
    return Promise.all([
      client.getEntries({
        'content_type': 'texts'
      })
    ]).then(([texts]) => {
      return {
        texts: texts.items[0]
      }
    }).catch(console.error)
  }
}
</script>

<style lang="stylus">
.about
  line-height 1rem
  p
    margin 1.5rem 0
</style>