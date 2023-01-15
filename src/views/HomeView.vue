<template>
  <AddTask v-show="showAddTask" @add-task="addTask" />
  <TaskItems
    @toggle-reminder="toggleReminder"
    @delete-task="deleteTask"
    :tasks="tasks"
  />
</template>

<script>
import TaskItems from "../components/TaskItems.vue";
import AddTask from "../components/AddTask.vue";

export default {
  name: "HomeView",
  props: {
    showAddTask: Boolean,
  },
  components: {
    TaskItems,
    AddTask,
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    async fetchTasks() {
      const response = await fetch("api/tasks");

      const data = await response.json();

      return data;
    },
    async fetchTask(id) {
      const response = await fetch(`api/tasks/${id}`);

      const data = await response.json();

      return data;
    },
    async addTask(task) {
      const response = await fetch("api/tasks", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(task),
      });

      const data = await response.json();

      this.tasks = [...this.tasks, data];
    },
    async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id);
      const updatedTask = { ...taskToToggle, reminder: !taskToToggle.reminder };

      const response = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(updatedTask),
      });

      const data = await response.json();

      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: data.reminder } : task
      );
    },
    async deleteTask(id) {
      if (confirm("Are you sure you want to delete?")) {
        const response = await fetch(`api/tasks/${id}`, {
          method: "DELETE",
        });

        response.status === 200
          ? (this.tasks = this.tasks.filter((task) => task.id !== id))
          : alert("Error deleting task.");
      }
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script>

<style scoped></style>
