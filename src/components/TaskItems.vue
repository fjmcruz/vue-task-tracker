<template>
  <div :key="task.id" v-for="task in tasks">
    <TaskItem
      @toggle-reminder="$emit('toggle-reminder', task.id)"
      @delete-task="$emit('delete-task', task.id)"
      :task="task"
    />
  </div>
</template>

<script>
import TaskItem from "./TaskItem.vue";

export default {
  name: "TaskItems",
  props: {
    tasks: Array,
  },
  components: {
    TaskItem,
  },
  emits: ["toggle-reminder", "delete-task"],
};
</script>

<style scoped></style>
