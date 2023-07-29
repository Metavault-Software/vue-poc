<script setup>
import {FormKitSchema} from '@formkit/vue'
import {ref} from 'vue'
import {OpenAiChatSchema} from './OpenAiChatSchema/OpenAiChatSchema';

const jsonData = ref({
  "tasks": [
    {
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
    }
  ]
});

let schema = OpenAiChatSchema(jsonData.value);
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
      :data="jsonData"
  />
</template>
