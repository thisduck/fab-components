<script setup lang="ts">
defineProps<{
  name: string;
  type?: string;
  placeholder?: string;
}>();
</script>

<template>
  <FabField
    :name="name"
    :placeholder="placeholder"
    :type="type || 'text'"
    as="textarea"
    class="py-2 px-3 rounded-md border border-gray-600 w-full"
  >
    <template v-if="$slots.label" #label>
      <slot name="label"></slot>
    </template>
  </FabField>
</template>
