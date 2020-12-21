<template>
  <div>
    <div class="four_rows">
      <div class="rows">
        <div class="row">
          <Work 
            v-for="work in works.slice(0, Math.floor(works.length/4))" 
            :key="work.sys.id"
            :work="work"
          />
        </div>
        <div class="row">
          <Work 
            v-for="work in works.slice(Math.floor(works.length/4), Math.floor(works.length/4)*2+Math.max(0,works.length%4-2))" 
            :key="work.sys.id"
            :work="work"
          />
        </div>
        <div class="row">
          <Work 
            v-for="work in works.slice(Math.floor(works.length/4)*2+Math.max(0,works.length%4-2), Math.floor(works.length/4)*3+works.length%4+Math.max(0,works.length%4-2))" 
            :key="work.sys.id"
            :work="work"
          />
        </div>
        <div class="row">
          <Work 
            v-for="work in works.slice(Math.floor(works.length/4)*3+works.length%4)" 
            :key="work.sys.id"
            :work="work"
          />
        </div>
      </div>
    </div>
    <div class="three_rows">
      <div class="rows">
        <div class="row">
          <Work 
            v-for="work in works.slice(0, Math.floor(works.length/3)+works.length%3)" 
            :key="work.sys.id"
            :work="work"
          />
        </div>
        <div class="row">
          <Work 
            v-for="work in works.slice(Math.floor(works.length/3)+works.length%3, Math.floor(works.length/3)*2+works.length%3)" 
            :key="work.sys.id"
            :work="work"
          />
        </div>
        <div class="row">
          <Work 
            v-for="work in works.slice(Math.floor(works.length/3)*2+works.length%3)" 
            :key="work.sys.id"
            :work="work"
          />
        </div>
      </div>
    </div>
    <div class="two_rows">
      <div class="rows">
        <div class="row">
          <Work 
            v-for="work in works.slice(0, Math.floor(works.length/2)+works.length%2)" 
            :key="work.sys.id"
            :work="work"
          />
        </div>
        <div class="row">
          <Work 
            v-for="work in works.slice(Math.floor(works.length/2)+works.length%2)" 
            :key="work.sys.id"
            :work="work"
          />
        </div>
      </div>
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

<style lang="stylus"> 

.rows
  display flex
  flex-wrap wrap
  justify-content flex-start

.three_rows, .two_rows
  display none 
@media(max-width 1200px)
  .four_rows
    display none
  .three_rows
    display block
@media(max-width 1100px)
  .two_rows
    display block
  .three_rows
    display none


.row
  width calc(15%+80px)
  margin 0 0.2rem
  transition .2s
  @media(max-width 1200px)
    width calc(20%+100px)
  @media(max-width 1100px)
    width 48%

</style>