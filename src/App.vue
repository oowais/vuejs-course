<template>
  <div class="container">
    <Header @toggle-add-task="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask"/>
    <router-view :showAddTask="showAddTask"></router-view>
    <Footer/>
  </div>
</template>

<script>
import {Options, Vue} from 'vue-class-component';
import Header from '@/components/Header.vue';
import Footer from "@/components/Footer";

@Options({
  components: {
    Footer,
    Header,
  },
  data() {
    return {
      showAddTask: false,
    }
  },
  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    },
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
