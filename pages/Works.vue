<template>
  <div>
    <div class="four_rows">
      <div class="rows">
        <div class="row">
          <Work 
            v-for="work in works.slice(0, list_four[0])" 
            :key="work.sys.id"
            :work="work"
          />
        </div>
        <div class="row">
          <Work 
            v-for="work in works.slice(list_four[0], list_four[0]+list_four[1])" 
            :key="work.sys.id"
            :work="work"
          />
        </div>
        <div class="row">
          <Work 
            v-for="work in works.slice(list_four[0]+list_four[1], list_four[0]+list_four[1]+list_four[2])" 
            :key="work.sys.id"
            :work="work"
          />
        </div>
        <div class="row">
          <Work 
            v-for="work in works.slice(list_four[0]+list_four[1]+list_four[2])" 
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
            v-for="work in works.slice(0, list_three[0])"
            :key="work.sys.id"
            :work="work"
          />
        </div>
        <div class="row">
          <Work 
            v-for="work in works.slice(list_three[0], list_three[0]+list_three[1])" 
            :key="work.sys.id"
            :work="work"
          />
        </div>
        <div class="row">
          <Work 
            v-for="work in works.slice(list_three[0]+list_three[1])" 
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
            v-for="work in works.slice(0, list_two[0])" 
            :key="work.sys.id"
            :work="work"
          />
        </div>
        <div class="row">
          <Work 
            v-for="work in works.slice(list_two[0])" 
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
    function partition(dividend, n) {
      var base = Math.floor(dividend / n)
      var rem  = dividend % n
      var list = []
      for (var i = 0; i<n; i++) {
        list[i] = (i < rem) ? base + 1 : base
      }
      return list
    }
    return Promise.all([
      client.getEntries({
        'content_type': 'work',
        order: 'fields.date'
      })
    ]).then(([works]) => {
      return {
        works: works.items,
        list_two: partition(works.items.length,2),
        list_three: partition(works.items.length,3),
        list_four: partition(works.items.length,4)
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
@media(max-width 1000px)
  .two_rows
    display block
  .three_rows
    display none

.row
  width calc(15%+80px)
  margin 0 0.15rem
  transition .2s
  @media(max-width 1200px)
    width calc(20%+80px)
  @media(max-width 1000px)
    width 48%
  @media(max-width 670px)
    width 100%


</style>