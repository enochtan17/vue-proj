<template>
  <header>
    <h1>{{ title }}</h1>
    <Button
      :text="showAddTask ? 'Close' : text"
      @toggle-add-task="$emit('toggle-add-task')"
    ></Button>
  </header>
</template>

<script>
  import Button from './Button'

  export default {
    name: 'Header',
    props: {
      title: {
        type: String,
        default: 'Hello World'
      },
      showAddTask: Boolean
    },
    components: {
      Button
    },
    data: () => ({
      text: 'Add Task'
    })
  }
</script>

<style scoped>
  
</style>
