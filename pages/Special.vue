<template>
  <div class="narrow">
    <img 
      :src="special.fields.media.fields.file.url" 
      class="w-full display-block mx-auto"
    >
  </div>
</template>

<script>
import { createClient } from '~/plugins/contentful.js'
const client = createClient()
export default { 
  asyncData() {
    return Promise.all([
      client.getEntries({
        'content_type': 'special'
      })
    ]).then(([specials]) => {
      return {
        special: specials.items[0]
      }
    }).catch(console.error)
  }
}
</script>

<style lang="stylus">
.about
  p
    margin 1.5rem 0
</style>