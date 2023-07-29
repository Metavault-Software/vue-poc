<template>
  <div class="OpenAiChatSchema">
    <pre v-text="$attrs"/>
  </div>
</template>

<script>
export const OpenAiChatSchema = (json) => {
  return json.tasks.map((task, index) => {
    return {
      $el: 'section',
      children: [
        {
          $formkit: 'group',
          id: `task${index}`,
          name: `task${index}`,
          children: [
            {
              $formkit: 'text',
              name: `task${index}.id`,
              label: '*Task ID',
              placeholder: 'Task ID',
              validation: 'required',
              value: task.id,
              props: {readonly: true},
            },
            {
              $formkit: 'text',
              name: `task${index}.name`,
              label: '*Task Name',
              placeholder: 'Task Name',
              validation: 'required',
              value: task.name,
              props: {readonly: true},
            },
            {
              $formkit: 'text',
              name: `task${index}.executor`,
              label: '*Executor',
              placeholder: 'Executor',
              validation: 'required',
              value: task.executor,
              props: {readonly: true},
            },
            {
              $el: 'div',
              children: task.args.messages.map((message, messageIndex) => {
                return {
                  $el: 'div',
                  children: [
                    {
                      $formkit: 'text',
                      name: `task${index}.args.messages[${messageIndex}].role`,
                      label: 'Role',
                      value: message.role,
                      props: {readonly: true},
                    },
                    {
                      $formkit: 'textarea',
                      name: `task${index}.args.messages[${messageIndex}].content`,
                      label: 'Content',
                      value: message.content,
                      props: {readonly: true},
                    },
                  ],
                };
              }),
            },
            {
              $formkit: 'button',
              type: 'submit',
              label: 'Submit',
              props: {
                class: 'btn btn-primary',
              },
            }
          ],
        },
      ],
    };
  });
};
</script>
