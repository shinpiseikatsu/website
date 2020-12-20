<template>
  <header>
    <div class="menu_btn cursor-pointer" @click="nav = true">
      <img src="../assets/img/icon_2.jpg" alt="">
    </div>
    <div v-if="nav == true" class="bg" @click="nav = false"></div>
    <nav :class="{'nav_on': nav == true}">
      <nuxt-link to="/">
        <li :class="{'active': $route.path == '/'}" @click="nav = false">works</li>
      </nuxt-link>
      <nuxt-link to="/products">
        <li :class="{'active': $route.path == '/products'}" @click="nav = false">products</li>
      </nuxt-link>
      <nuxt-link to="/about">
        <li :class="{'active': $route.path == '/about'}" @click="nav = false">about us</li>
      </nuxt-link>
      <nuxt-link to="/contact">
        <li :class="{'active': $route.path == '/contact'}" @click="nav = false">contact</li>
      </nuxt-link>
    </nav>
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
  max-width 80%
  width 400px
  margin-right -400px
  position fixed
  top 0
  bottom 0
  right 0
  box-shadow 0 0 5px rgba(0,0,0,.1) 
  background white
  padding-top 3rem
  transition .2s
  z-index 100
  li
    list-style none
    font-size 2.5rem
    padding 1.5rem 2rem
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