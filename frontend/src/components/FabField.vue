<script setup lang="ts">
import { ErrorMessage } from 'vee-validate';
import { computed } from 'vue';
import startCase from 'lodash/startCase';

const props = defineProps<{
  name: string;
  label?: string;
  help?: string;
  labelAfter?: boolean;
  inputWrapperClasses?: string;
}>();

const labelValue = computed(() => {
  return props.label ?? startCase(props.name.split('.').reverse()[0]);
});
</script>

<script lang="ts">
export default {
  inheritAttrs: false,
};
</script>

<template>
  <div class="mb-4">
    <FabLabel v-if="props.label !== 'false' && !labelAfter" :for="name">
      <slot v-if="$slots.label" name="label"></slot>
      <span v-else>
        {{ labelValue }}
      </span>
    </FabLabel>
    <div :class="inputWrapperClasses">
      <slot name="default"></slot>
      <FabLabel v-if="props.label !== 'false' && labelAfter" :for="name">
        <slot v-if="$slots.label" name="label"></slot>
        <span v-else>
          {{ labelValue }}
        </span>
      </FabLabel>
    </div>
    <p v-if="help" class="mt-1 block text-gray-700 text-sm">{{ help }}</p>
    <ErrorMessage :name="name" class="mt-1 block text-error-600 text-sm" />
  </div>
</template>
