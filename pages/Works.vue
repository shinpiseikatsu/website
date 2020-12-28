<template>
  <div>
    <div class="four_cols">
      <div class="cols">
        <div class="col">
          <Work 
            v-for="work in works.slice(0, list_four[0])" 
            :key="work.sys.id"
            :work="work"
          />
        </div>
        <div class="col">
          <Work 
            v-for="work in works.slice(list_four[0], list_four[0]+list_four[1])" 
            :key="work.sys.id"
            :work="work"
          />
        </div>
        <div class="col">
          <Work 
            v-for="work in works.slice(list_four[0]+list_four[1], list_four[0]+list_four[1]+list_four[2])" 
            :key="work.sys.id"
            :work="work"
          />
        </div>
        <div class="col">
          <Work 
            v-for="work in works.slice(list_four[0]+list_four[1]+list_four[2])" 
            :key="work.sys.id"
            :work="work"
          />
        </div>
      </div>
    </div>
    <div class="three_cols">
      <div class="cols">
        <div class="col">
          <Work 
            v-for="work in works.slice(0, list_three[0])"
            :key="work.sys.id"
            :work="work"
          />
        </div>
        <div class="col">
          <Work 
            v-for="work in works.slice(list_three[0], list_three[0]+list_three[1])" 
            :key="work.sys.id"
            :work="work"
          />
        </div>
        <div class="col">
          <Work 
            v-for="work in works.slice(list_three[0]+list_three[1])" 
            :key="work.sys.id"
            :work="work"
          />
        </div>
      </div>
    </div>
    <div class="two_cols">
      <div class="cols">
        <div class="col">
          <Work 
            v-for="work in works.slice(0, list_two[0])" 
            :key="work.sys.id"
            :work="work"
          />
        </div>
        <div class="col">
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