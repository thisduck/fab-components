<script setup lang="ts">
// empty

async function handleSubmit(event) {
  // console.log(event);
  let count = 1;

  while (count < 3) {
    console.log(count);
    await new Promise(resolve => setTimeout(resolve, 500));
    count += 1;
  }
}
</script>

<template>
  <div class="mt-12 text-center text-slate-800">
    <RandomForm class="space-x-4" @submit="handleSubmit">
      <input name="companyName" class="py-2 px-3 rounded-md border border-gray-600" />
      <RandomButton>Submit</RandomButton>
      <RandomButton disabled type="button">Cancel</RandomButton>
    </RandomForm>
  </div>
</template>
