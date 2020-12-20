<template>
  <header>
    <nuxt-link to="/special">
      <div class="logo">
        <img src="../assets/img/icon_1.jpg" alt="">
      </div>
      <nav class="mt-5">
        <li>
          <nuxt-link to="/">products</nuxt-link>
        </li>
        <li>
          <nuxt-link to="/works">works</nuxt-link>
        </li>
        <li>
          <nuxt-link to="/about">about</nuxt-link>
        </li>
        <li>
          <nuxt-link to="/contact">contact</nuxt-link>
        </li>
      </nav>
    </nuxt-link>
  </header>
</template>

<script>
import { createClient } from '~/plugins/contentful.js'
const client = createClient()
export default { 
  data() {
    return {
      nav: false
    }
  },
  asyncData() {
    return Promise.all([
      client.getEntries({
        'content_type': 'siteInfo'
      })
    ]).then(([siteInfo]) => {
      return {
        siteInfo: siteInfo.items[0]
      }
    }).catch(console.error)
  }
}
</script>

<style lang="stylus" scoped>
header
  padding 2rem 0
nav
  li
    list-style none
    font-size 1rem
    padding .5rem 0
  .active
    font-weight bold

.menu_btn 
  position fixed
  top 1rem
  right 1rem
  width 3rem
  img 
    width 100%
.nav_on 
  margin-right 0
.bg
  position fixed
  top 0
  bottom 0
  width 100%
  background rgba(255,255,255,.8)
  z-index 50
</style>