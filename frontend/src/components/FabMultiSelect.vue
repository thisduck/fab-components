<script setup lang="ts">
import { computed } from 'vue';
import Multiselect from '@vueform/multiselect';

const props = defineProps<{
  options: Record<string, string> | string[];
  mode?: 'single' | 'multiple' | 'tags';
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
  <FabField class="h-5 w-5 rounded-md border border-gray-600 mt-px">
    <template #default="{ field }">
      <Multiselect
        v-model="field.value.value"
        :options="optionsValue"
        :mode="mode || 'single'"
        :hideSelected="mode === 'tags'"
        :searchable="true"
      />
      <input
        type="hidden"
        :name="field.name"
        :id="field.name"
        v-model="field.value.value"
        @input="field.handleChange"
        @blur="field.handleBlur"
      />
    </template>
    <template v-if="$slots.label" #label>
      <slot name="label"></slot>
    </template>
  </FabField>
</template>

<style src="@vueform/multiselect/themes/default.css"></style>
