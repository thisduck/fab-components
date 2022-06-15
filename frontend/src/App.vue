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
    <RandomForm v-slot="{ isRunning }" class="space-x-4" @submit="handleSubmit">
      <pre>{{ isRunning }}</pre>
      <input name="companyName" class="rounded-md border border-gray-600 py-2 px-3" />
      <RandomButton>Submit</RandomButton>
      <RandomButton disabled type="button">Cancel</RandomButton>
    </RandomForm>
  </div>
</template>
