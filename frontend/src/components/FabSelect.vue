<script setup lang="ts">
import { Field } from 'vee-validate';
import { useAttrs, computed } from 'vue';

const props = defineProps<{
  name: string;
  label?: string;
  placeholder?: string;
  help?: string;
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

const attrs = useAttrs();
</script>

<script lang="ts">
export default {
  inheritAttrs: false,
};
</script>

<template>
  <FabField :label="label" :help="help" :name="name">
    <Field
      as="select"
      :id="name"
      :name="name"
      :validateOnBlur="false"
      :validateOnChange="false"
      class="py-2 px-3 rounded-md border border-gray-600 w-full"
      v-bind="attrs"
    >
      <option v-if="placeholder" value="">
        {{ placeholder }}
      </option>
      <option v-for="[value, label] of Object.entries(optionsValue)" :key="value" :value="value">
        {{ label }}
      </option>
    </Field>
    <template v-if="$slots.label" #label>
      <slot name="label"></slot>
    </template>
  </FabField>
</template>
