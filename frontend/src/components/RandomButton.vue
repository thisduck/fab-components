<script setup lang="ts">
import { inject, defineProps, computed, Ref } from 'vue';

const props = defineProps<{
  type?: 'submit' | 'button' | 'reset';
  disabled?: boolean;
}>();

const formIsRunning: Ref<boolean> = inject('formIsRunning');

const disabledValue = computed(() => {
  return props.disabled || isRunning.value;
});

const isSubmitType = computed(() => {
  return !props.type || props.type === 'submit';
});

const isRunning = computed(() => {
  return isSubmitType.value && formIsRunning.value;
});
</script>

<template>
  <button
    :disabled="disabledValue"
    :type="props.type"
    class="inline-flex flex-row items-center space-x-2 rounded-md border border-gray-600 bg-blue-700 py-2 px-3 text-gray-100 transition-all"
  >
    <MdiLoading v-if="isRunning" class="h-6 w-6 animate-spin text-red-600" />
    <span v-else class="block"><slot></slot></span>
  </button>
</template>

<style scoped>
button[disabled] {
  @apply bg-gray-200 text-gray-800;
}
</style>
