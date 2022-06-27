<script setup lang="ts"></script>

<template>
  <FabField
    :label-after="true"
    input-wrapper-classes="flex flex-row space-x-2"
    type="checkbox"
    class="mt-px w-5 h-5 rounded-md border border-gray-600"
  >
    <template v-if="$slots.label" #label>
      <slot name="label"></slot>
    </template>
  </FabField>
</template>
