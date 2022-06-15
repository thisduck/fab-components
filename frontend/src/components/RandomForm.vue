<script setup lang="ts">
import { useTask } from 'vue-concurrency';
import { useAttrs, provide, toRef } from 'vue';

const attrs = useAttrs();

const { onSubmit, ...restOfAttrs } = attrs;

const submitTask = useTask(function* (_signal, event: Event) {
  yield (onSubmit as (event: Event) => void)(event);
}).drop();

provide('formIsRunning', toRef(submitTask, 'isRunning'));
</script>

<script lang="ts">
export default {
  inheritAttrs: false,
};
</script>

<template>
  <form v-bind="restOfAttrs" @submit.prevent="event => submitTask.perform(event)">
    <slot :task="submitTask"></slot>
  </form>
</template>
