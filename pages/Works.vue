<template>
  <div class="mt-5 flex flex-wrap">
    <Work 
      v-for="work in works" 
      :key="work.sys.id"
      :work="work"
    />
  </div>
</template>

<script>
import Work from '@/components/Work'
import { createClient } from '~/plugins/contentful.js'
const client = createClient()
export default { 
  components: {
    Work
  },
  asyncData() {
    return Promise.all([
      client.getEntries({
        'content_type': 'work',
        order: 'fields.date'
      })
    ]).then(([works]) => {
      return {
        works: works.items
      }
    }).catch(console.error)
  }
}
</script>

<style lang="stylus">
.logo
  width 8rem
  img 
    width 100%  
</style>