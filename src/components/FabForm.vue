<script setup lang="ts">
import { useTask } from 'vue-concurrency';
import { useAttrs, provide, toRef } from 'vue';
import { Form, SubmissionContext } from 'vee-validate';
import FabModal from './FabModal.vue';

const attrs = useAttrs();

const props = defineProps<{
  confirmationModalRef?: InstanceType<typeof FabModal>;
}>();

const { onSubmit, ...restOfAttrs } = attrs;

const submitTask = useTask(function* (_signal, ...args) {
  yield (onSubmit as any)(...args);
}).drop();

type Values = Record<string, unknown>;

async function submitWrapper(values: Values, ctx: SubmissionContext<Values>) {
  if (props.confirmationModalRef) {
    const confirmation = await props.confirmationModalRef.show<boolean>();
    if (!confirmation) return;
  }
  submitTask.perform(values, ctx);
}

provide('formIsRunning', toRef(submitTask, 'isRunning'));
</script>

<script lang="ts">
export default {
  inheritAttrs: false,
};
</script>

<template>
  <Form
    v-slot="formParams"
    v-bind="restOfAttrs"
    @submit="(values, context) => submitWrapper(values, context)"
  >
    <slot v-bind="formParams" :task="submitTask"></slot>
  </Form>
</template>
