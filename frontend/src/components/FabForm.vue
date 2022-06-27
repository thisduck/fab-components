<script setup lang="ts">
import { useTask } from 'vue-concurrency';
import { useAttrs, provide, toRef } from 'vue';
import { Form } from 'vee-validate';

const attrs = useAttrs();

const { onSubmit, ...restOfAttrs } = attrs;

const submitTask = useTask(function* (_signal, values: any) {
  yield (onSubmit as (values: any) => void)(values);
}).drop();

provide('formIsRunning', toRef(submitTask, 'isRunning'));
</script>

<script lang="ts">
export default {
  inheritAttrs: false,
};
</script>

<template>
  <Form v-bind="restOfAttrs" @submit="values => submitTask.perform(values)" v-slot="formParams">
    <slot v-bind="formParams" :task="submitTask"></slot>
  </Form>
</template>
