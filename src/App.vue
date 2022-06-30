<template>
  <div class="app">
    <Header :showAdd="showAddTask" @handleClick="toggleShow" />
    <div v-show="showAddTask">
      <AddTask @add-task="addTask" />
    </div>
    <Tasks
      :tasks="tasks"
      @delete-task="deleteTask"
      @toggle-complete="toggleComplete"
    />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Tasks from "./components/Tasks.vue";
import AddTask from "./components/AddTask.vue";
import { URL } from "../config";

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
    };
  },

  methods: {
    async addTask(newTask) {
      const res = await fetch(`${URL}/tasks`, {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(newTask),
      });

      const data = await res.json();
      this.tasks = [...this.tasks, data];
    },
    async deleteTask(id) {
      if (confirm("Are you Sure")) {
        const res = await fetch(`${URL}/tasks/${id}`, {
          method: "DELETE",
        });

        res.status === 200
          ? (this.tasks = this.tasks.filter((task) => task.id !== id))
          : alert("Error Deleting Task");
      }
    },
    toggleShow() {
      this.showAddTask = !this.showAddTask;
    },
    async toggleComplete(id) {
      const taskToToggle = await this.fetchTask(id);
      const updateTask = {
        ...taskToToggle,
        completed: !taskToToggle.completed,
      };

      const res = await fetch(`${URL}/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(updateTask),
      });

      const data = await res.json();

      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, completed: data.completed } : task
      );
    },

    async fetchTasks() {
      const res = await fetch(`${URL}/tasks`);
      const data = await res.json();
      return data;
    },
    async fetchTask(id) {
      const res = await fetch(`${URL}/tasks/${id}`);
      const data = await res.json();
      return data;
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script>

<style scoped>
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 50vw;
  margin: auto;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
}
</style>
