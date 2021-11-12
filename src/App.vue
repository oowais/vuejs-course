<template>
  <div class="container">
    <Header @toggle-add-task="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask"/>
    <div>
      <AddTask v-show="showAddTask" @add-task="addTask"/>
    </div>
    <Tasks @delete-task="deleteTask" @toggle-reminder="toggleReminder" :tasks="tasks"/>
  </div>
</template>

<script>
import {Options, Vue} from 'vue-class-component';
import Header from '@/components/Header.vue';
import Tasks from '@/components/Tasks.vue';
import AddTask from '@/components/AddTask.vue';

@Options({
  components: {
    AddTask,
    Header,
    Tasks
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
    }
  },
  methods: {
    async deleteTask(id) {
      if (confirm('Are you sure?')) {
        const res = await fetch(`api/tasks/${id}`, {
          method: 'DELETE',
        })

        res.status === 200 ? this.tasks = this.tasks.filter((task) => task.id != id) : alert('Error deleting task')

      }
    },
    async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id)
      const updatedTask = {...taskToToggle, reminder: !taskToToggle.reminder}

      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(updatedTask),
      })

      const data = await res.json()

      this.tasks = this.tasks.map((task) =>
          task.id === id ? {...task, reminder: data.reminder} : task)
    },
    async addTask(task) {
      const res = await fetch(`api/tasks`, {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(task),
      })

      const data = await res.json()

      this.tasks = [...this.tasks, data]
    },
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    },
    async fetchTasks() {
      const res = await fetch(`api/tasks`)

      const data = await res.json()

      return data
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`)

      const data = await res.json()

      return data
    }
  },
  async created() {
    this.tasks = await this.fetchTasks()
  }
})
export default class App extends Vue {
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Poppins', sans-serif;
}

.container {
  max-width: 500px;
  margin: 2em auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 2em;
  border-radius: 5px;
}

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn:focus {
  outline: none;
}

.btn:active {
  transform: scale(0.98);
}

.btn-block {
  display: block;
  width: 100%;
}
</style>
