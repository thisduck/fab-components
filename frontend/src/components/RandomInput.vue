<script setup lang="ts">
import { Field, ErrorMessage } from 'vee-validate';
import { useAttrs, computed } from 'vue';
import startCase from 'lodash/startCase';

const props = defineProps<{
  name: string;
  type?: string;
  placeholder?: string;
  label?: string;
  help?: string;
}>();

const labelValue = computed(() => {
  return props.label ?? startCase(props.name.split('.').reverse()[0]);
});
const attrs = useAttrs();
</script>

<script lang="ts">
export default {
  inheritAttrs: false,
};
</script>

<template>
  <div class="mb-4">
    <label v-if="props.label !== 'false'" :for="name" class="block text-sm mb-1">
      {{ labelValue }}
    </label>
    <Field
      :id="name"
      :name="name"
      :type="type || 'text'"
      :placeholder="placeholder"
      :validateOnBlur="false"
      class="py-2 px-3 rounded-md border border-gray-600"
      v-bind="attrs"
    />
    <ErrorMessage :name="name" class="mt-1 block text-error-600 text-sm" />
    <p v-if="help" class="mt-1 block text-gray-700 text-sm">{{ help }}</p>
  </div>
</template>
