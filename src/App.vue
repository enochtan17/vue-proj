<template>
  <div id="app">
    <Header
      @toggle-add-task="toggleAddTask"
      :title="title"
      :showAddTask="showAddTask"
    ></Header>
    <div
      v-show="showAddTask"
    >
      <AddTask
      :tasks="tasks"
      @add-task="addTask"
      ></AddTask>
    </div>
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
import AddTask from './components/AddTask'

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask,
  },
  data: () => ({
    title: 'Task Tracker',
    tasks: [],
    showAddTask: false
  }),
  methods: {
    deleteTask(id) {
      if (confirm('Are you sure?')) {
        this.tasks = this.tasks.filter(task => task.id != id)
      }
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map(task => {
        if (task.id == id) {
          return {
            ...task,
            reminder: !task.reminder
          }
        } else return task
      })
    },
    async fetchTasks() {
      const res = await fetch('http://localhost:5000/tasks')

      const data = await res.json()

      return data
    },
    addTask(newTask) {
      this.tasks = [...this.tasks, newTask]
    },
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    }
  },
  async created() {
    this.tasks = await this.fetchTasks()
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
