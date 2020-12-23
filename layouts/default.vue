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
@import url('https://fonts.googleapis.com/css2?family=Quicksand:wght@300;500;700&display=swap')

html
  font-family 'Quicksand', 'Yu Gothic', 'YuGothic', sans-serif
  font-size 14px
  word-spacing 1px
  padding 3rem
  @media (max-width 670px)
    padding 3rem 1rem

aside
  width 150px
  padding 2rem 0
  @media (max-width 670px)
    width 100%
    padding 0

main
  width 75%
  padding 1rem 0
  margin 0 auto
  @media (max-width 670px)
    width 100%
</style>
