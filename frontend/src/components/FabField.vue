<script setup lang="ts">
import { ErrorMessage, useField } from 'vee-validate';
import { computed } from 'vue';
import startCase from 'lodash/startCase';

const props = defineProps<{
  name: string;
  type?: string;
  label?: string;
  help?: string;
  labelAfter?: boolean;
  inputWrapperClasses?: string;
  onLabelClick?: () => void;
  checkedValue?: unknown;
  uncheckedValue?: unknown;
}>();

const fieldParams = useField(props.name, undefined, {
  type: props.type,
  checkedValue: props.checkedValue ?? true,
  valueProp: props.checkedValue ?? false,
  uncheckedValue: props.uncheckedValue ?? false,
});

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
    <FabLabel v-if="props.label !== 'false' && !labelAfter" :for="name" @click="onLabelClick">
      <slot v-if="$slots.label" name="label"></slot>
      <span v-else>{{ labelValue }}</span>
    </FabLabel>
    <div :class="inputWrapperClasses">
      <slot name="default" v-bind="{ field: fieldParams }"></slot>
      <FabLabel v-if="props.label !== 'false' && labelAfter" :for="name" @click="onLabelClick">
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
