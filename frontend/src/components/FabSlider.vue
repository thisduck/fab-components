<script setup lang="ts">
import { ref } from 'vue';
import Slider from '@vueform/slider';

defineProps<{
  name: string;
}>();

const value = ref<number | number[]>(0);
</script>

<template>
  <FabField :name="name" v-model="value">
    <template #default="{ field }">
      <Slider v-model="value" :labelledby="name" />
      <input type="hidden" v-bind="field" />
    </template>
    <template v-if="$slots.label" #label>
      <slot name="label"></slot>
    </template>
  </FabField>
</template>

<style src="@vueform/slider/themes/default.css"></style>
