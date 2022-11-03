<template>
  <div>
    <div
      v-for="task in tasks"
      :key="task.id"
    >
      <Task
        @toggle-reminder="$emit('toggle-reminder', task.id)"
        @delete-task="$emit('delete-task', task.id)"
        :task="task"
      ></Task>
  </div>
</div>
</template>

<script>
  import Task from './Task'

  export default {
    name: "tasks",
    props: {
        tasks: {
            type: Array,
            default: []
        }
    },
    methods: {
        onClick() {
            console.log("click");
        }
    },
    components: {
      Task
    },
}
</script>
