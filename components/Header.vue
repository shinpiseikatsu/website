<template>
  <header>
    <nuxt-link to="/special">
      <div class="logo">
        <img src="../assets/img/icon_1.jpg" alt="">
      </div>
    </nuxt-link>
    <nav class="nav_lg">
      <li :class="{'active': $route.path == '/'}">
        <nuxt-link to="/">PRODUCTS</nuxt-link>
      </li>
      <li :class="{'active': $route.path == '/works'}">
        <nuxt-link to="/works">WORKS</nuxt-link>
      </li>
      <li :class="{'active': $route.path == '/about'}">
        <nuxt-link to="/about">ABOUT</nuxt-link>
      </li>
      <li :class="{'active': $route.path == '/contact'}">
        <nuxt-link to="/contact">CONTACT</nuxt-link>
      </li>
      <li>
        <nuxt-link to="/contact">INSTAGRAM</nuxt-link>
      </li>
    </nav>
    <div class="menu_btn cursor-pointer" @click="nav = !nav">
      <span v-if="!nav">menu</span>
      <span v-else>close</span>
    </div>
    <nav v-if="nav == true" class="nav_sm">
      <li :class="{'active': $route.path == '/'}" @click="nav = false">
        <nuxt-link to="/">PRODUCTS</nuxt-link>
      </li>
      <li :class="{'active': $route.path == '/works'}" @click="nav = false">
        <nuxt-link to="/works">WORKS</nuxt-link>
      </li>
      <li :class="{'active': $route.path == '/about'}" @click="nav = false">
        <nuxt-link to="/about">ABOUT</nuxt-link>
      </li>
      <li :class="{'active': $route.path == '/contact'}" @click="nav = false">
        <nuxt-link to="/contact">CONTACT</nuxt-link>
      </li>
      <li>
        <nuxt-link to="/contact" @click="nav = false">INSTAGRAM</nuxt-link>
      </li>
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
  position fixed
  top 3rem
  left 3rem
  @media(max-width 670px) 
    position relative
    top 0
    left 0
    margin-bottom 2rem
.logo
  width 6rem
  @media(max-width 670px) 
    margin 0 auto
.nav_lg
  margin-top 1.25rem
  li
    list-style none
    font-size .8rem
    padding .5rem 0
  .active
    font-weight bold
  @media(max-width 670px) 
    display none
.menu_btn 
  position fixed
  top 1rem
  right 1rem
  width 3rem
  z-index 100
.nav_sm
  position fixed
  top 0
  bottom 0
  width 100%
  background white
  padding 3rem
  z-index 50
  li
    list-style none
    font-size 2rem
    padding .5rem 0
  .active
    font-weight bold
</style>