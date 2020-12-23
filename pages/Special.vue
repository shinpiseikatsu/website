<template>
  <div>
    {{randomInt}}
    <img 
      :src="special.fields.images[randomInt].fields.file.url" 
      class="w-full display-block mx-auto"
    >
    <p class="mt-12" v-if="special.fields.text" >{{ special.fields.text }}</p>
  </div>
</template>

<script>
import { createClient } from '~/plugins/contentful.js'
const client = createClient()
export default { 
  asyncData() {
    function getRandomInt(max) {
      return Math.floor(Math.random() * Math.floor(max));
    }
    return Promise.all([
      client.getEntries({
        'content_type': 'special'
      })
    ]).then(([specials]) => {
      return {
        special: specials.items[0],
        randomInt: getRandomInt(specials.items[0].fields.images.length)
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