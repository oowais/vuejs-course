<template>
  <div @dblclick="$emit('toggle-reminder', task.id)" :class="[task.reminder ? 'reminder' : '', 'task']">
    <h3>
      {{ task.text }}
      <i @click="onDelete(task.id)" class="fas fa-times"></i>
    </h3>
    <p>{{ task.day }}</p>
  </div>
</template>

<script>

export default {
  name: "Task",
  props: {
    task: Object,
  }, methods: {
    onDelete(id) {
      this.$emit('delete-task', id);
    },
  },
}
</script>

<style scoped>
.fas {
  color: red;
}

.task {
  background: #f4f4f4;
  margin: 0.25em;
  padding: 0.5em 1em;
  cursor: pointer;
}

.task.reminder {
  border-left: 0.25em solid green;
}

.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
