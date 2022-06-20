<script setup lang="ts">
import { Field } from 'vee-validate';
import { useAttrs } from 'vue';

defineProps<{
  name: string;
  type?: string;
  placeholder?: string;
  label?: string;
  help?: string;
}>();

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
      :id="name"
      :name="name"
      :type="type || 'text'"
      :placeholder="placeholder"
      :validateOnBlur="false"
      :validateOnChange="false"
      class="py-2 px-3 rounded-md border border-gray-600"
      v-bind="attrs"
    />
    <template v-if="$slots.label" #label>
      <slot name="label"></slot>
    </template>
  </FabField>
</template>
