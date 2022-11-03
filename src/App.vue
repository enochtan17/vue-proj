<template>
  <div id="app">
    <Header
      :title="title"
    ></Header>
    <Tasks
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask"
      :tasks="tasks"
    ></Tasks>
  </div>
</template>

<script>
import Header from './components/Header'
import Tasks from './components/Tasks'

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    Tasks
  },
  data: () => ({
    title: 'Task Tracker',
    tasks: []
  }),
  methods: {
    deleteTask(id) {
      if (confirm('Are you sure?')) {
        this.tasks = this.tasks.filter(task => task.id != id)
      }
    },
    toggleReminder(id) {
      console.log('reminder', id)
    }
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Groceries',
        day: 'October 26',
        reminder: true
      },
      {
        id: 2,
        text: 'Meeting',
        day: 'November 3',
        reminder: true
      },
      {
        id: 3,
        text: 'Pay rent',
        day: 'December 1',
        reminder: false
      },
    ]
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
