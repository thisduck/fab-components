<script setup lang="ts">
import { computed } from 'vue';

const props = defineProps<{
  placeholder?: string;
  options: Record<string, string> | string[];
}>();

const optionsValue = computed(() => {
  if (Array.isArray(props.options)) {
    return props.options.reduce((acc, value) => {
      return {
        ...acc,
        [value]: value,
      };
    }, {});
  }
  return props.options;
});
</script>

<template>
  <FabField>
    <template #default="{ field }">
      <select
        :name="field.name"
        :id="field.name"
        v-model="field.value.value"
        @input="field.handleChange"
        @blur="field.handleBlur"
        class="py-2 px-3 rounded-md border border-gray-600 w-full"
      >
        <option v-if="placeholder" value="">
          {{ placeholder }}
        </option>
        <option v-for="[value, label] of Object.entries(optionsValue)" :key="value" :value="value">
          {{ label }}
        </option>
      </select>
    </template>
    <template v-if="$slots.label" #label>
      <slot name="label"></slot>
    </template>
  </FabField>
</template>
