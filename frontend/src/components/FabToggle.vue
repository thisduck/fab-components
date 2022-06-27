<script setup lang="ts">
import { ref } from 'vue';
import Toggle from '@vueform/toggle';

defineProps<{
  name: string;
}>();

const value = ref();
</script>

<template>
  <FabField
    :name="name"
    :label-after="true"
    input-wrapper-classes="flex flex-row flex-row-reverse justify-between"
    class="h-5 w-5 rounded-md border border-gray-600 mt-px"
    v-model="value"
    @label-click="value = !value"
  >
    <template #default="{ field }">
      <Toggle v-model="value" :labelledby="name" />
      <input type="hidden" v-bind="field" />
    </template>
    <template v-if="$slots.label" #label>
      <slot name="label"></slot>
    </template>
  </FabField>
</template>

<style src="@vueform/toggle/themes/default.css"></style>
