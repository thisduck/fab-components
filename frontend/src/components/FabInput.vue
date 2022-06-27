<script setup lang="ts">
defineProps<{
  type?: string;
  placeholder?: string;
}>();
</script>

<template>
  <FabField
    :placeholder="placeholder"
    :type="type || 'text'"
    class="py-2 px-3 rounded-md border border-gray-600 w-full"
  >
    <template v-if="$slots.label" #label>
      <slot name="label"></slot>
    </template>
  </FabField>
</template>
