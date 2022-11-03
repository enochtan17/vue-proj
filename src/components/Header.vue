<template>
  <header>
    <h1>{{ title }}</h1>
    <Button
      :text="text"
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
      }
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
