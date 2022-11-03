<template>
  <div
    @dblclick="$emit('toggle-reminder', task.id)"
    :class="[ task.reminder ? 'reminder' : '' ]"
  >
    <h3>
      {{ task.text }}
      <i @click="onDelete(task.id)" class="fas fa-times"></i>
    </h3>
    <p>{{ task.day }}</p>
  </div>
</template>

<script>
  export default {
    name: 'Task',
    props: {
      task: {
        type: Object,
        default: {}
      }
    },
    methods: {
      onDelete(id) {
        this.$emit('delete-task', id)
      }
    }
  }
</script>

<style>
  .fas {
    color: red;
  }
  .reminder {
    border-left: 200px green solid;
  }
</style>
