<script setup lang="ts">
import { useTask } from 'vue-concurrency';
import { useAttrs, provide, toRef } from 'vue';
import { Form } from 'vee-validate';

const attrs = useAttrs();

const { onSubmit, ...restOfAttrs } = attrs;

const submitTask = useTask(function* (_signal, ...args) {
  yield (onSubmit as any)(...args);
}).drop();

provide('formIsRunning', toRef(submitTask, 'isRunning'));
</script>

<script lang="ts">
export default {
  inheritAttrs: false,
};
</script>

<template>
  <Form v-slot="formParams" v-bind="restOfAttrs" @submit="(...args) => submitTask.perform(...args)">
    <slot v-bind="formParams" :task="submitTask"></slot>
  </Form>
</template>
