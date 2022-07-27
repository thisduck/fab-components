<script setup lang="ts">
import { ref } from 'vue';
import { FieldArray } from 'vee-validate';
import { string, object, array, boolean } from 'yup';

const showModal = ref(false);

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
  termsOfAgreement: boolean().label('Terms Of Agreement'),
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
  <div class="p-4">
    <FabButton size="xs" type="button" @click="showModal = true">Open Modal</FabButton>
    <pre>{{ showModal }}</pre>
    <FabModal :show="showModal" @close="showModal = false">
      <template #title>Payment successful</template>
      <template #default>
        <div class="mt-2">
          <p class="text-sm text-gray-500">
            Your payment has been successfully submitted. We’ve sent you an email with all of the
            details of your order.
          </p>
        </div>

        <div class="mt-4">
          <button
            type="button"
            class="inline-flex justify-center rounded-md border border-transparent bg-blue-100 px-4 py-2 text-sm font-medium text-blue-900 hover:bg-blue-200 focus:outline-none focus-visible:ring-2 focus-visible:ring-blue-500 focus-visible:ring-offset-2"
            @click="showModal = false"
          >
            Got it, thanks!
          </button>
        </div>
      </template>
    </FabModal>
  </div>
  <div class="mt-12 text-slate-800">
    <FabForm
      class="p-4 w-1/3"
      @submit="handleSubmit"
      :validation-schema="schema"
      :initial-values="{
        firstName: 'Person',
        location: 'Teeheehee',
        oldColor: 'green',
        color: ['red'],
        colors: ['red', 'green'],
        termsOfAgreement: true,
        light: true,
        width: 30,
        blogpost: 'I ate eggs.',
        companies: [{ setting: { companyName: 'name@inc.com' }, location: 'LalaLand' }],
        hidden: 'hiddenValue',
      }"
    >
      <FabInput :name="`firstName`" help="Your first name" />

      <div class="mb-4">
        <FabInput :name="`location`" />
      </div>
      <div class="mb-4">
        <FabSelect
          name="oldColor"
          placeholder="Please select a color"
          :options="{
            orange: 'Orange',
            red: 'Red Things',
            green: 'Green Stuff',
          }"
        />
      </div>
      <div class="mb-4">
        <FabMultiSelect
          name="color"
          placeholder="Please select a color"
          :options="{
            orange: 'Orange',
            red: 'Red Things',
            green: 'Green Stuff',
          }"
          mode="multiple"
        />
      </div>
      <div class="mb-4">
        <FabMultiSelect :name="`colors`" :options="['orange', 'green', 'red']" mode="tags" />
      </div>
      <div class="mb-4">
        <FabCheckbox :name="`termsOfAgreement`">
          <template #label>
            Please
            <em>carefully</em>
            read over all the terms of agreement, and accept or you will be held accountable. lollz.
          </template>
        </FabCheckbox>
      </div>
      <div class="mb-4">
        <FabToggle :name="`light`"></FabToggle>
      </div>
      <div class="mb-4">
        <FabSlider :name="`width`" :value="30"></FabSlider>
      </div>
      <div class="mb-4">
        <FabTextarea :name="`blogpost`" />
      </div>
      <FabHidden :name="`hidden`" />
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
        <FabButton size="base" variant="outline" type="button">Submit</FabButton>
        <FabButton size="xs" type="button">Xtra-Small</FabButton>
        <FabButton size="sm" color="error" type="button">Small</FabButton>
      </div>
    </FabForm>
  </div>
</template>
