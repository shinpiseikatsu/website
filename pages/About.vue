<template>
  <div class="narrow">
    <h2 class="text-5xl my-2">新皮生活</h2>
    <div 
      v-html="$md.render(about.fields.messageJp)"
      class="about leading-loose"
    ></div>
    <h2 class="text-5xl my-2">Shinpiseikatsu</h2>
    <div 
      v-html="$md.render(about.fields.messageEn)"
      class="about leading-loose"
    ></div>
  </div>
</template>

<script>
import Member from '@/components/Member'
import { createClient } from '~/plugins/contentful.js'
const client = createClient()
export default { 
  components: {
    Member
  },
  asyncData() {
    return Promise.all([
      client.getEntries({
        'content_type': 'about'
      }),
      client.getEntries({
        'content_type': 'member'
      })
    ]).then(([abouts,members]) => {
      return {
        about: abouts.items[0],
        members: members
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