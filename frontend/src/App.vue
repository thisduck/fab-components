<script setup lang="ts">
import { FieldArray } from 'vee-validate';
import { string, object, array } from 'yup';

async function handleSubmit(values: any) {
  console.log(values);

  let count = 1;

  while (count < 3) {
    console.log(count);
    await new Promise(resolve => setTimeout(resolve, 500));
    count += 1;
  }
}

const validateEmail = string().email().required();
const schema = object({
  companies: array().of(
    object({
      setting: object({
        companyName: validateEmail.label('Company Name'),
      }),
      location: string().required().label('Location'),
    })
  ),
});
</script>

<template>
  <div class="mt-12 text-slate-800">
    <FabForm class="p-4" @submit="handleSubmit" :validation-schema="schema">
      <FabInput label="false" :name="`firstName`" help="Your first name" />

      <div class="mb-4">
        <FabInput :name="`location`" />
      </div>
      <FieldArray v-slot="{ fields, push, remove }" name="companies">
        <div v-for="(field, index) of fields" :key="field.key" class="mb-4">
          <FabInput
            label="false"
            :name="`companies[${index}].setting.companyName`"
            help="The name of your company"
          />

          <div class="mb-4">
            <FabInput :name="`companies[${index}].location`" />
          </div>

          <div>
            <FabButton size="xs" type="button" @click="remove(index)">- remove</FabButton>
          </div>
        </div>
        <FabButton size="xs" type="button" @click="push({})">+ Company</FabButton>
      </FieldArray>

      <div class="pt-4 space-x-4">
        <FabButton>Submit</FabButton>
        <FabButton size="xs" type="button">Xtra-Small</FabButton>
        <FabButton size="sm" type="button">Small</FabButton>
        <FabButton size="base" type="button">Base</FabButton>
      </div>
    </FabForm>
  </div>
</template>
