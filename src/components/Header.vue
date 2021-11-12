<template>
  <header>
    <h1>{{ title }}</h1>
    <Button v-show="homePage" @btn-click="$emit('toggle-add-task')" :text="showAddTask ? 'Close' : 'Add Task'"
            :color="showAddTask? 'red' : 'green'"/>
  </header>
</template>

<script>
import Button from '@/components/Button.vue';

export default {
  name: "Header",
  components: {Button},
  computed: {
    homePage() {
      return this.$route.path === '/';
    }
  },
  props: {
    title: {
      type: String,
      default: 'Default header value'
    },
    showAddTask: Boolean,
  },
  emits: ['toggle-add-task']
}
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2em;
}
</style>
