<template>
  <div class="narrow">
    <form 
      name="contact" 
      method="POST" 
      netlify
    >
      <input type="hidden" name="form-name" value="contact" /> 
      <input 
        type="name" 
        name="name"
        placeholder="name"
        required 
      >
      <input 
        type="text" 
        name="title"
        placeholder="title"
        required 
      >
      <input 
        type="email" 
        name="email" 
        placeholder="email"
        required 
      >
      <textarea 
        name="message" 
        rows="10" 
        placeholder="message"
        required
      ></textarea>
      <p class="my-5">{{ texts.fields.contactMessage }}</p>
      <button type="submit">Send</button>
    </form>
  </div>
</template>

<script>
import { createClient } from '~/plugins/contentful.js'
const client = createClient()
export default { 
  asyncData() {
    return Promise.all([
      client.getEntries({
        'content_type': 'texts'
      })
    ]).then(([texts]) => {
      return {
        texts: texts.items[0]
      }
    }).catch(console.error)
  }
}
</script>

<style lang="stylus" scope>
input, textarea
  line-height 1.5
  background white
  border none
  border-bottom 2px solid gray
  padding 1rem
  width 100%
  transition .1s
  border-radius 0
input:focus, textarea:focus
  outline none
  border-bottom 2px solid black
  font-weight bold
input::placeholder, textarea::placeholder
  color black
  opacity 1
button 
  display block
  width fit-content
  padding .5rem 3rem
  margin 0 auto
  border 2px solid black 
  border-radius 2rem
</style>