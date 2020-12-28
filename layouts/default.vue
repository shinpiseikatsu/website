<template>
  <div class="flex flex-wrap justify-around">
    <aside>
      <Header />
    </aside>
    <main>
      <nuxt />
    </main>
  </div>
</template>

<script>
import Header from '@/components/Header'
export default {
  components: {
    Header
  }
}
</script>

<style lang="stylus">

html
  font-family 'Quicksand', 'Yu Gothic', 'YuGothic', sans-serif
  font-size 14px
  word-spacing 1px
  padding 3rem 0
  @media (max-width 900px)
    padding 3rem 1rem
aside
  width 180px
  padding 2rem 0
  @media (max-width 900px)
    width 100%
    padding 0
main
  width 80%
  padding 1rem 0
  margin 0 auto
  @media (max-width 900px)
    width 100%
.narrow
  width 700px
  max-width 80%
  margin 0 auto
  @media (max-width 900px)
    width 100%
    max-width 100%
button:focus
  border none!important
  outline none!important
</style>
