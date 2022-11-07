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

const api = 'http://localhost:5000/tasks'

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
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    },
    async fetchTasks() {
      const res = await fetch(`${api}`)

      const data = await res.json()

      return data
    },
    async fetchTask(id) {
      const res = await fetch(`${api}/${id}`)

      const data = await res.json()

      return data
    },
    async addTask(task) {
      const res = await fetch(`${api}`, {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(task)
      })

      const data = await res.json()

      this.tasks = [...this.tasks, data]
    },
    async deleteTask(id) {
      if (confirm('Are you sure?')) {
        const res = await fetch(`${api}/${id}`, {
          method: 'DELETE'
        })

        res.status === 200
          ? this.tasks = this.tasks.filter(task => task.id != id)
          : alert('Error deleting task')
      }
    },
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
