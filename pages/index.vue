<template>
  <div>
    <nuxt-link to="/special">
      <div class="logo">
        <img src="../assets/img/icon_1.jpg" alt="">
      </div>
    </nuxt-link>
    <div class="mt-5 flex flex-wrap justify-around w-full">
      <Work 
        v-for="work in works" 
        :key="work.sys.id"
        :work="work"
      />
    </div>
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