<script setup lang="ts">
import { useTask } from 'vue-concurrency';
import { useAttrs } from 'vue';

const attrs = useAttrs();

const { onSubmit, ...restOfAttrs } = attrs;

const submitTask = useTask(function* (_signal, event: Event) {
  yield (onSubmit as (event: Event) => void)(event);
}).drop();
</script>

<script lang="ts">
export default {
  inheritAttrs: false,
};
</script>

<template>
  <form v-bind="restOfAttrs" @submit.prevent="event => submitTask.perform(event)">
    <slot></slot>
  </form>
</template>
