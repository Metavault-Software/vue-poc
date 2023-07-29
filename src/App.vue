<script setup>
import {FormKitSchema} from '@formkit/vue'
import {ref} from 'vue'

const data = ref({
  email: '',
  password: '',
  password_confirm: '',
  eu_citizen: false,
  cookie_notice: '',
})
const schema = []
const jsonData = {
  "id": "1",
  "name": "OpenAI Chat Task",
  "executor": "OpenAIAgent",
  "args": {
    "messages": [
      {
        "role": "user",
        "content": "Write a Go program to illustrate Go's powerful concurrency model."
      }
    ]
  }
};
const jsonToSchema = (json) => {
  return [
    {
      $formkit: 'text',
      name: 'id',
      label: 'ID',
      help: 'This is the ID of the task.',
      validation: 'required',
      value: json.id,
      props: {readonly: true}
    },
    {
      $formkit: 'text',
      name: 'name',
      label: 'Name',
      help: 'This is the name of the task.',
      validation: 'required',
      value: json.name,
      props: {readonly: true}
    },
    {
      $formkit: 'text',
      name: 'executor',
      label: 'Executor',
      help: 'This is the executor of the task.',
      validation: 'required',
      value: json.executor,
      props: {readonly: true}
    },
    {
      $formkit: 'textarea',
      width: '100%',
      height: '400px',
      name: 'args',
      label: 'Arguments',
      help: 'These are the arguments of the task.',
      validation: 'required',
      value: JSON.stringify(json.args, null, 2),
      props: {readonly: true}
    },
    {
      $formkit: 'submit',
      label: 'Submit',
      props: {class: 'btn btn-primary'}
    }
  ];
}
const newSchemaEntries = jsonToSchema(jsonData);
newSchemaEntries.forEach(entry => schema.push(entry));

const createCharacter = async (fields) => {
  await new Promise((r) => setTimeout(r, 1000))
  alert(JSON.stringify(fields))
}
</script>

<style>
[data-invalid] .formkit-inner {
  border-color: red;
  box-shadow: 0 0 0 1px red;
}

[data-complete] .formkit-inner {
  border-color: red;
  box-shadow: 0 0 0 1px green;
}

[data-complete] .formkit-inner::after {
  content: '✅';
  display: block;
  padding: 0.5em;
}
</style>

<template>
  <FormKitSchema
      type="form"
      @submit="createCharacter"
      :schema="schema"
      :data="data"
  />
  <p>{{ data.email }}</p>
</template>
