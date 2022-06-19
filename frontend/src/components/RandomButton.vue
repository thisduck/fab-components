<script setup lang="ts">
import { inject, defineProps, computed, Ref, ref, watch } from 'vue';

const props = defineProps<{
  type?: 'submit' | 'button' | 'reset';
  disabled?: boolean;
  size?: 'xs' | 'sm' | 'base';
}>();

const formIsRunning: Ref<boolean> | undefined = inject('formIsRunning');

const disabledValue = computed(() => {
  return props.disabled || isRunning.value;
});

const isSubmitType = computed(() => {
  return !props.type || props.type === 'submit';
});

const isRunning = computed(() => {
  return isSubmitType.value && formIsRunning?.value;
});

const width = ref(0);
const buttonRef = ref();

watch(isRunning, (newValue, oldValue) => {
  if (!oldValue && newValue) {
    width.value = buttonRef.value.offsetWidth;
  } else {
    width.value = 0;
  }
});

const size = computed(() => {
  return props.size || 'base';
});

const buttonClasses = computed(() => {
  const classes: string[] = [];
  const buttonSizes = {
    xs: 'py-1 px-2 text-xs',
    sm: 'py-1.5 px-2.5 text-sm',
    base: 'py-2 px-3 text-base',
  };
  classes.push(buttonSizes[size.value]);
  return classes;
});
</script>

<template>
  <button
    ref="buttonRef"
    :disabled="disabledValue"
    :type="props.type"
    class="inline-flex items-center justify-center space-x-2 rounded-md bg-primary-700 text-gray-100 transition-all shadow-md hover:bg-primary-600 focus:ring-primary-400 focus:ring-offset-2 focus:ring-2"
    :class="[{ running: isRunning }, buttonClasses]"
    :style="width ? `width: ${width}px` : ''"
  >
    <span v-if="isRunning" class="inline-block">
      <GgSpinner class="inline-block h-6 w-6 animate-spin text-gray-100" />
    </span>
    <span v-else class="inline-block"><slot></slot></span>
  </button>
</template>

<style scoped>
button[disabled] {
  @apply opacity-50 cursor-not-allowed;
}
button[disabled].running {
  @apply opacity-100;
}
</style>
