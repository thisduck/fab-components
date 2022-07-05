<script setup lang="ts">
defineProps<{
  name: string;
  type?: string;
  placeholder?: string;
}>();
</script>

<template>
  <FabField :name="name">
    <template #default="{ field }">
      <textarea
        :name="field.name"
        :id="field.name"
        v-model="field.value.value"
        @input="field.handleChange"
        @blur="field.handleBlur"
        :placeholder="placeholder"
        :type="type || 'text'"
        class="py-2 px-3 rounded-md border border-gray-600 w-full"
      />
    </template>
    <template v-if="$slots.label" #label>
      <slot name="label"></slot>
    </template>
  </FabField>
</template>
