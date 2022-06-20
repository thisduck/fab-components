<script setup lang="ts">
import { Field } from 'vee-validate';
import { useAttrs } from 'vue';

defineProps<{
  name: string;
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
  <FabField
    :label="label"
    :help="help"
    :name="name"
    :label-after="true"
    input-wrapper-classes="flex flex-row space-x-2"
  >
    <Field
      :id="name"
      :name="name"
      type="checkbox"
      :validateOnBlur="false"
      :validateOnChange="false"
      class="h-5 w-5 rounded-md border border-gray-600 mt-px"
      v-bind="attrs"
    />
    <template v-if="$slots.label" #label>
      <slot name="label"></slot>
    </template>
  </FabField>
</template>
