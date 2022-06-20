<script setup lang="ts">
defineProps<{
  for: string;
}>();
</script>

<template>
  <label :for="for" class="block text-sm mb-1">
    <slot></slot>
  </label>
</template>
