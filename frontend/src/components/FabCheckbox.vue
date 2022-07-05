<script setup lang="ts">
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
    input-wrapper-classes="flex flex-row space-x-2"
    type="checkbox"
    :checkedValue="value"
    :uncheckedValue="uncheckedValue"
  >
    <template #default="{ field }">
      <input
        :id="field.name"
        :name="field.name"
        type="checkbox"
        class="mt-px w-5 h-5 rounded-md border border-gray-600"
        :checked="field.value.value === field.checkedValue"
        @input="
          field.value.value = $event.target?.checked ? field.checkedValue : field.uncheckedValue
        "
        @blur="field.handleBlur"
      />
    </template>
    <template v-if="$slots.label" #label>
      <slot name="label"></slot>
    </template>
  </FabField>
</template>
