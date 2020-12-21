<template>
  <div class="narrow">
    <input 
      class="bg-white focus:outline-none focus:border-black border-b border-gray-300 py-4 px-4 block w-full appearance-none leading-normal" 
      type="name" 
      placeholder="name"
    >
    <input 
      class="bg-white focus:outline-none focus:border-black border-b border-gray-300 py-4 px-4 block w-full appearance-none leading-normal" 
      type="text" 
      placeholder="title"
    >
    <input 
      class="bg-white focus:outline-none focus:border-black border-b border-gray-300 py-4 px-4 block w-full appearance-none leading-normal" 
      type="email" 
      placeholder="email"
    >
    <textarea 
      class="bg-white focus:outline-none focus:border-black border-b border-gray-300 py-4 px-4 block w-full appearance-none leading-normal"
      name="message" 
      rows="10" 
      placeholder="message"
    ></textarea>
    <p class="my-5">{{ texts.fields.contactMessage }}</p>
    <div class="py-2 px-4 border border-gray-400 text-gray-400 cursor-pointer my-3 mx-auto w-32 text-center">send</div>
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