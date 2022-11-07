<template>
  <form
    class="add-form"
    @submit="onSubmit"
  >
    <div class="form-control">
      <label>Task</label>
      <input
        v-model="text"
        type="text"
        name="text"
        placeholder="Add Task"
      />
    </div>
    <div class="form-control">
      <label>Day</label>
      <input
        v-model="day"
        type="text"
        name="day"
        placeholder="Add Day"
      />
    </div>
    <div class="form-control form-control-check">
      <label>Set Reminder</label>
      <input
        v-model="reminder"
        type="checkbox"
        name="reminder"
      />
    </div>
    <input
      type="submit"
      value="Save Task"
      class="btn btn-block"
    />
  </form>
</template>

<script>
  export default {
    name: 'AddTask',
    data() {
      return {
        text: '',
        day: '',
        reminder: false
      }
    },
    props: {
      tasks: {
        type: Array,
        default: []
      }
    },
    methods: {
      clearForm() {
        this.text = ''
        this.day = ''
        this.reminder = false
      },
      // nextId() {
      //   const ids = this.tasks.map(task => task.id)

      //   return Math.max(...ids) + 1
      // },
      onSubmit(e) {
        e.preventDefault()

        if(!this.text) {
          alert('Please add a task!')
          return 
        }

        const newTask = {
          // id: this.nextId(),
          text: this.text,
          day: this.day,
          reminder: this.reminder
        }

        this.$emit('add-task', newTask)

        this.clearForm()
      },
    }
  }
</script>
