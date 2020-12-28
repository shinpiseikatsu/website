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
      <div>
        <div class="btn_wrapper" :class="{ 'open': nav }">
          <span></span>
          <span></span>
          <span></span>
        </div>
      </div>
    </div>
    <nav class="nav_sm" :class="{ 'open': nav }">
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
  @media(max-width 900px) 
    position relative
    top 0
    left 0
    margin-bottom 2rem
.logo
  width 6rem
  @media(max-width 900px) 
    margin 0 auto
.nav_lg
  margin-top 1.25rem
  li
    list-style none
    font-size .8rem
    padding .5rem 0
  .active
    font-weight bold
  @media(max-width 900px) 
    display none
.menu_btn 
  position fixed
  top 1rem
  right 2.5rem
  width 2.5rem
  z-index 100
  .btn_wrapper
    width 60px
    height 45px
    position relative
    margin 0 auto
    -webkit-transform rotate(0deg) scale(0.5,0.5)
    -moz-transform rotate(0deg) scale(0.5,0.5)
    -o-transform rotate(0deg) scale(0.5,0.5)
    transform rotate(0deg) scale(0.5,0.5)
    -webkit-transition .5s ease-in-out
    -moz-transition .5s ease-in-out
    -o-transition .5s ease-in-out
    transition .5s ease-in-out
    cursor pointer
    span
      display block
      position absolute
      height 3px
      width 100%
      background black
      border-radius: 9px
      opacity 1
      left 0
      -webkit-transform rotate(0deg)
      -moz-transform rotate(0deg)
      -o-transform rotate(0deg)
      transform rotate(0deg)
      -webkit-transition .25s ease-in-out
      -moz-transition .25s ease-in-out
      -o-transition .25s ease-in-out
      transition .25s ease-in-out
  .btn_wrapper span:nth-child(1)
    top 0px
  .btn_wrapper span:nth-child(2)
    top 18px
  .btn_wrapper span:nth-child(3)
    top 36px
  .btn_wrapper.open span:nth-child(1)
    top 18px
    -webkit-transform rotate(135deg)
    -moz-transform rotate(135deg)
    -o-transform rotate(135deg)
    transform rotate(135deg)
  .btn_wrapper.open span:nth-child(2)
    opacity 0
    left -60px
  .btn_wrapper.open span:nth-child(3)
    top 18px
    -webkit-transform rotate(-135deg)
    -moz-transform rotate(-135deg)
    -o-transform rotate(-135deg)
    transform rotate(-135deg)
  @media(min-width 900px) 
    display none
.nav_sm
  position fixed
  top 0
  bottom 0
  width 100%
  background white
  padding 3rem
  z-index -10
  opacity 0
  -webkit-transition .25s ease-in-out
  -moz-transition .25s ease-in-out
  -o-transition .25s ease-in-out
  transition .25s ease-in-out
  @media(min-width 900px) 
    display none
  li
    list-style none
    font-size 2rem
    padding .5rem 0
  .active
    font-weight bold
.nav_sm.open
  opacity 1
  display block
  z-index 50
  @media(min-width 900px) 
    display none
</style>