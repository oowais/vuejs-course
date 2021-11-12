<template>
  <div class="container">
    <Header @toggle-add-task="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask"/>
    <div>
      <AddTask v-show="showAddTask" @add-task="addTask"/>
    </div>
    <Tasks @delete-task="deleteTask" @toggle-reminder="toggleReminder" :tasks="tasks"/>
  </div>
</template>

<script lang="ts">
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
    deleteTask(id: number): void {
      if (confirm('Are you sure?')) {
        this.tasks = this.tasks.filter((task: any) => task.id != id)
      }
    },
    toggleReminder(id: number): void {
      this.tasks = this.tasks.map((task: any) =>
          task.id === id ? {...task, reminder: !task.reminder} : task)
    },
    addTask(task: any) {
      this.tasks = [...this.tasks, task]
    },
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    }
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Doctors Appointment',
        day: 'March 1st at 2:30pm',
        reminder: true,
      },
      {
        id: 2,
        text: 'Meeting at School',
        day: 'March 3rd at 1:30pm',
        reminder: true,
      },
      {
        id: 3,
        text: 'Grocery Shopping',
        day: 'March 3rd at 11:00am',
        reminder: false,
      },

    ]
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
