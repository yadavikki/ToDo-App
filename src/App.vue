<template>
  <div id="app">
    <h1>ToDo List App</h1>
    <form @submit.prevent="addTask">
      <input v-model="newTask" placeholder="Add a new task" />
      <button type="submit">Add Task</button>
    </form>

    <h2>Open Tasks</h2>
    <ul>
      <li v-for="task in openTasks" :key="task.id">
        <span>{{ task.title }}</span>
        <span>Created on: {{ formatDate(task.createdAt) }}</span>
        <button @click="completeTask(task.id)">Complete</button>
      </li>
    </ul>

    <h2>Completed Tasks</h2>
    <ul>
      <li v-for="task in completedTasks" :key="task.id">
        <span>{{ task.title }}</span>
        <span>Completed on: {{ formatDate(task.completedAt) }}</span>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      newTask: "",
      tasks: [],
    };
  },
  mounted() {
    this.fetchTasks();
  },
  methods: {
    async fetchTasks() {
      const response = await axios.get("http://localhost:3000/tasks");
      this.tasks = response.data;
    },
    async addTask() {
      if (this.newTask.trim() !== "") {
        const response = await axios.post("http://localhost:3000/tasks", {
          title: this.newTask,
          createdAt: new Date(),
          completed: false,
          completedAt: null,
        });

        this.tasks.push(response.data);
        this.newTask = "";
      }
    },
    async completeTask(taskId) {
      const task = this.tasks.find((t) => t.id === taskId);
      if (task) {
        task.completed = true;
        task.completedAt = new Date();
        await axios.put(`http://localhost:3000/tasks/${taskId}`, task);
      }
    },
    formatDate(date) {
      const options = { year: "numeric", month: "long", day: "numeric" };
      return new Date(date).toLocaleDateString("en-US", options);
    },
  },
  computed: {
    openTasks() {
      return this.tasks.filter((task) => !task.completed);
    },
    completedTasks() {
      return this.tasks.filter((task) => task.completed);
    },
  },
};
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background-color: #f0f0f0; 
  padding: 20px; 
}

h1 {
  font-size: 2em;
  margin-bottom: 20px;
}

form {
  margin-bottom: 20px;
}

input {
  padding: 10px;
  margin-right: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  padding: 10px;
  background-color: #3498db;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin: 10px 0;
  padding: 15px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #ecf0f1;
}

li span {
  display: block;
}

button:hover {
  background-color: #2980b9;
}
</style>

