<script setup lang="ts">
import Slider from '@vueform/slider';

defineProps<{
  name: string;
}>();

// TODO: add min/max settings from slider component.
// handle initial multi values?
</script>

<template>
  <FabField :name="name">
    <template #default="{ field }">
      <Slider v-model="field.value.value" :labelledby="name" />
      <input
        :name="field.name"
        :id="field.name"
        v-model="field.value.value"
        @input="field.handleChange"
        @blur="field.handleBlur"
        type="hidden"
      />
    </template>
    <template v-if="$slots.label" #label>
      <slot name="label"></slot>
    </template>
  </FabField>
</template>

<style src="@vueform/slider/themes/default.css"></style>
