<script setup lang="ts">
import Toggle from '@vueform/toggle';

defineProps<{
  name: string;
  value?: unknown;
  uncheckedValue?: unknown;
}>();
</script>

<template>
  <FabField
    :name="name"
    :label-after="true"
    input-wrapper-classes="flex flex-row flex-row-reverse justify-between"
    type="checkbox"
    :checkedValue="value"
    :uncheckedValue="uncheckedValue"
  >
    <template #default="{ field }">
      <Toggle
        v-model="field.value.value"
        :labelledby="name"
        :falseValue="field.uncheckedValue"
        :trueValue="field.checkedValue"
      />
      <input
        :id="field.name"
        :name="field.name"
        type="checkbox"
        class="hidden"
        :checked="field.value.value === field.checkedValue"
        @input="
          field.value.value = ($event.target as HTMLInputElement | null)?.checked
            ? field.checkedValue
            : field.uncheckedValue
        "
        @blur="field.handleBlur"
      />
    </template>
    <template v-if="$slots.label" #label>
      <slot name="label"></slot>
    </template>
  </FabField>
</template>

<style src="@vueform/toggle/themes/default.css"></style>
