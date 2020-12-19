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
    <div class="py-2 px-4 border border-gray-400 text-gray-400 cursor-pointer my-3 mx-auto w-32 text-center">send</div>
  </div>
</template>