<script setup lang="ts"></script>

<template>
  <FabField label="false" type="hidden">
    <template v-if="$slots.label" #label>
      <slot name="label"></slot>
    </template>
  </FabField>
</template>
