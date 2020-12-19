<template>
  <div>
    <Header />
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

main
  padding 1rem 2% 8rem

.narrow
  width 100%
  max-width 600px
  margin 0 auto

.logo
  width 13rem
  margin 0 auto
  img 
    width 100%
</style>
