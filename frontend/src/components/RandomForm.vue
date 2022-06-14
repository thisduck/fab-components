<script setup lang="ts">
// empty

const emit = defineEmits(['submit']);

function submit(event) {
  emit('submit', event);
}
</script>

<template>
  <form class="space-x-4" @submit.prevent="submit">
    <slot></slot>
  </form>
</template>
