<script setup lang="ts">
import { Field } from 'vee-validate';
import { useAttrs, ref, computed } from 'vue';
import Multiselect from '@vueform/multiselect';

const props = defineProps<{
  name: string;
  label?: string;
  help?: string;
  options: Record<string, string> | string[];
  mode?: 'single' | 'multiple' | 'tags';
}>();

const attrs = useAttrs();
const value = ref();

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
      :validateOnBlur="false"
      :validateOnChange="false"
      class="h-5 w-5 rounded-md border border-gray-600 mt-px"
      v-bind="attrs"
      v-slot="{ field }"
      v-model="value"
    >
      <Multiselect
        v-model="value"
        :options="optionsValue"
        :mode="mode || 'single'"
        :hideSelected="mode === 'tags'"
        :searchable="true"
      />
      <input type="hidden" v-bind="field" />
    </Field>
    <template v-if="$slots.label" #label>
      <slot name="label"></slot>
    </template>
  </FabField>
</template>

<style src="@vueform/multiselect/themes/default.css"></style>
