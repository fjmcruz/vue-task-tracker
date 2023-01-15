<template>
  <div
    @dblclick="$emit('toggle-reminder', task.id)"
    :class="[task.reminder ? 'reminder' : '', 'task']"
  >
    <h2>
      {{ task.text }}
      <i @click="$emit('delete-task', task.id)" class="fas fa-times"></i>
    </h2>
    <p>{{ task.date }}</p>
  </div>
</template>

<script>
export default {
  name: "TaskItem",
  props: {
    task: Object,
  },
  emits: ["toggle-reminder", "delete-task"],
};
</script>

<style scoped>
.fas {
  color: salmon;
}

.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}

.task.reminder {
  border-left: 5px solid skyblue;
}

.task h2 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
