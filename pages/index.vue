<template>
  <div>
    <div class="four_cols">
      <div class="cols">
        <div class="col">
          <Product 
            v-for="product in products.slice(0, list_four[0])" 
            :key="product.sys.id"
            :product="product"
          />
        </div>
        <div class="col">
          <Product 
            v-for="product in products.slice(list_four[0], list_four[0]+list_four[1])" 
            :key="product.sys.id"
            :product="product"
          />
        </div>
        <div class="col">
          <Product 
            v-for="product in products.slice(list_four[0]+list_four[1], list_four[0]+list_four[1]+list_four[2])" 
            :key="product.sys.id"
            :product="product"
          />
        </div>
        <div class="col">
          <Product 
            v-for="product in products.slice(list_four[0]+list_four[1]+list_four[2])" 
            :key="product.sys.id"
            :product="product"
          />
        </div>
      </div>
    </div>
    <div class="three_cols">
      <div class="cols">
        <div class="col">
          <Product 
            v-for="product in products.slice(0, list_three[0])"
            :key="product.sys.id"
            :product="product"
          />
        </div>
        <div class="col">
          <Product 
            v-for="product in products.slice(list_three[0], list_three[0]+list_three[1])" 
            :key="product.sys.id"
            :product="product"
          />
        </div>
        <div class="col">
          <Product 
            v-for="product in products.slice(list_three[0]+list_three[1])" 
            :key="product.sys.id"
            :product="product"
          />
        </div>
      </div>
    </div>
    <div class="two_cols">
      <div class="cols">
        <div class="col">
          <Product 
            v-for="product in products.slice(0, list_two[0])" 
            :key="product.sys.id"
            :product="product"
          />
        </div>
        <div class="col">
          <Product 
            v-for="product in products.slice(list_two[0])" 
            :key="product.sys.id"
            :product="product"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Product from '@/components/Product'
import { createClient } from '~/plugins/contentful.js'
const client = createClient()
export default { 
  components: {
    Product
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
        'content_type': 'product',
        order: 'fields.date'
      })
    ]).then(([products]) => {
      return {
        products: products.items,
        list_two: partition(products.items.length,2),
        list_three: partition(products.items.length,3),
        list_four: partition(products.items.length,4)
      }
    }).catch(console.error)
  }
}
</script>

<style lang="stylus"> 

.cols
  display flex
  flex-wrap wrap
  justify-content flex-start
  @media(max-width 900px)
    justify-content center

.four_cols, .two_cols
  display none 
.three_cols
  display block
@media(max-width 1000px)
  .two_cols
    display block
  .three_cols
    display none

.col
  width calc(30%+20px)
  margin 0 0.15rem
  transition .2s
  @media(max-width 1000px)
    width 48%
  @media(max-width 700px)
    width 100%

</style>