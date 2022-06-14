<script setup lang="ts">
// empty

async function handleSubmit(event) {
  // console.log(event);
  let count = 1;

  while (count < 10) {
    console.log(count);
    await new Promise(resolve => setTimeout(resolve, 500));
    count += 1;
  }
}
</script>

<template>
  <div class="mt-12 text-center text-slate-800">
    <RandomForm class="space-x-4" @submit="handleSubmit">
      <input name="companyName" class="rounded-md border border-gray-600 py-2 px-3" />
      <button class="rounded-md border border-gray-600 py-2 px-3">Submit</button>
    </RandomForm>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
