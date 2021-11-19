<template>
  <nav class="bg-transparent p-6">
    <div class="max-w-6xl mx-auto px-4">
      <div class="flex justify-between">
        <div class="flex space-x-7">
          <div>
            <a href="#" class="flex items-center py-4 px-2">
              <img src="/logo.png" class="w-64"/>
            </a>
          </div>
        </div>
        <div class="flex items-center space-x-3">
          <button class="bg-transparent h-12 hover:bg-blue-500 text-blue-500 font-semibold hover:text-white py-2 px-4 border-4 border-blue-500 hover:border-transparent rounded text-mono">
            Setting
          </button>
          <button v-if="isLoggedIn" class="bg-transparent h-12 hover:bg-blue-500 text-blue-500 font-semibold hover:text-white py-2 px-4 border-4 border-blue-500 hover:border-transparent rounded text-mono">
            Dashboard
          </button>
          <button class="bg-transparent h-12 hover:bg-blue-500 text-blue-500 font-semibold hover:text-white py-2 px-4 border-4 border-blue-500 hover:border-transparent rounded text-mono">
            Login
          </button>          
        </div>
      </div>
    </div>
  </nav>
</template>

<script lang='ts'>
  import Component from 'vue-class-component';
  import Vue from 'vue';
  @Component({})
  export default class NavBarModal extends Vue {}
</script>