<script setup lang="ts">
import { FieldArray } from 'vee-validate';

async function handleSubmit(values: any) {
  console.log(values);

  let count = 1;

  while (count < 3) {
    console.log(count);
    await new Promise(resolve => setTimeout(resolve, 500));
    count += 1;
  }
}

function validateEmail(value: string) {
  // if the field is empty
  if (!value) {
    return 'This field is required';
  }
  // if the field is not a valid email
  const regex = /^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$/i;
  if (!regex.test(value)) {
    return 'This field must be a valid email';
  }
  // All is good
  return true;
}
</script>

<template>
  <div class="mt-12 text-slate-800">
    <RandomForm class="p-4" @submit="handleSubmit">
      <FieldArray v-slot="{ fields, push, remove }" name="companies">
        <div v-for="(field, index) of fields" :key="field.key" class="mb-4">
          <RandomInput
            label="false"
            :name="`companies[${index}].setting.companyName`"
            :rules="validateEmail"
            help="The name of your company"
          />

          <div class="mb-4">
            <RandomInput :name="`companies[${index}].location`" />
          </div>

          <div>
            <RandomButton size="xs" type="button" @click="remove(index)">- remove</RandomButton>
          </div>
        </div>
        <RandomButton size="xs" type="button" @click="push({})">+ Company</RandomButton>
      </FieldArray>

      <div class="pt-4 space-x-4">
        <RandomButton>Submit</RandomButton>
        <RandomButton size="xs" type="button">Xtra-Small</RandomButton>
        <RandomButton size="sm" type="button">Small</RandomButton>
        <RandomButton size="base" type="button">Base</RandomButton>
      </div>
    </RandomForm>
  </div>
</template>
