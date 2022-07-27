<script setup lang="ts">
import { useTask } from 'vue-concurrency';
import { useAttrs, provide, toRef } from 'vue';
import { Form } from 'vee-validate';
import FabModal from './FabModal.vue';

const attrs = useAttrs();

const props = defineProps<{
  confirmationModalRef?: InstanceType<typeof FabModal>;
}>();

const { onSubmit, ...restOfAttrs } = attrs;

const submitTask = useTask(function* (_signal, ...args) {
  yield (onSubmit as any)(...args);
}).drop();

async function submitWrapper(...args) {
  if (props.confirmationModalRef) {
    const confirmation = await props.confirmationModalRef.show<boolean>();
    if (!confirmation) return;
  }
  submitTask.perform(...args);
}

provide('formIsRunning', toRef(submitTask, 'isRunning'));
</script>

<script lang="ts">
export default {
  inheritAttrs: false,
};
</script>

<template>
  <Form v-slot="formParams" v-bind="restOfAttrs" @submit="(...args) => submitWrapper(...args)">
    <slot v-bind="formParams" :task="submitTask"></slot>
  </Form>
</template>
