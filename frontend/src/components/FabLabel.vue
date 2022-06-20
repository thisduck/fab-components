<script setup lang="ts">
const props = defineProps<{
  for: string;
}>();
</script>

<script lang="ts">
export default {
  inheritAttrs: false,
};
</script>

<template>
  <label :for="for" class="block text-sm mb-1">
    <slot></slot>
  </label>
</template>
