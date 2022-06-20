<script setup lang="ts">
import { Field } from 'vee-validate';
import { useAttrs, ref } from 'vue';
import Toggle from '@vueform/toggle';

defineProps<{
  name: string;
  label?: string;
  help?: string;
}>();

const attrs = useAttrs();
const value = ref();
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
    input-wrapper-classes="flex flex-row flex-row-reverse justify-between"
    @label-click="value = !value"
  >
    <Field
      :id="name"
      :name="name"
      :validateOnBlur="false"
      :validateOnChange="false"
      class="h-5 w-5 rounded-md border border-gray-600 mt-px"
      v-bind="attrs"
      v-slot="{ field }"
      v-model="value"
    >
      <Toggle v-model="value" :labelledby="name" />
      <input type="hidden" v-bind="field" />
    </Field>
    <template v-if="$slots.label" #label>
      <slot name="label"></slot>
    </template>
  </FabField>
</template>

<style src="@vueform/toggle/themes/default.css"></style>
