<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import HelloWorld from './components/HelloWorld.vue';
</script>

<template>
  <div class="mt-12 text-center text-slate-800">
    <div class="flex justify-center items-center">
      <MdiAccountBox class="w-12 h-12 text-green-500" />
    </div>

    <HelloWorld msg="Hello Vue 3 + TypeScript + Vite" />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
