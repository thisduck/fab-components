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
    class="inline-flex items-center justify-center space-x-2 rounded-md border border-gray-600 bg-blue-700 py-2 px-3 text-gray-100 transition-all"
  >
    <span v-if="isRunning" class="inline-block">
      <MdiLoading class="inline-block h-6 w-6 animate-spin text-red-600" />
    </span>
    <span v-else class="inline-block"><slot></slot></span>
  </button>
</template>

<style scoped>
button[disabled] {
  @apply bg-gray-200 text-gray-800;
}
</style>
