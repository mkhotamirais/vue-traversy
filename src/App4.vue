<script setup>
import { onMounted, ref } from "vue";

const name = ref("ahamd");
const status = ref("active");
const tasks = ref(["task 1", "task 2", "task 3"]);
const newTask = ref("");

const link = ref("https://google.com");

const toggleStatus = () => {
  if (status.value === "active") {
    status.value = "pending";
  } else if (status.value === "pending") {
    status.value = "inactive";
  } else {
    status.value = "active";
  }
};

const addTask = () => {
  tasks.value.push(newTask.value);
  newTask.value = "";
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

onMounted(async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos");
    const data = await response.json();
    tasks.value = data.map((task) => task.title);
  } catch (error) {
    console.log("error", error);
  }
});
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">user is active</p>
  <p v-else-if="status === 'pending'">user is pending</p>
  <p v-else>user is inactive</p>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" v-model="newTask" />
    <button type="submit">Add</button>
  </form>

  <h3>Tasks</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>
        {{ task }}
      </span>
      <button @click="deleteTask(index)">Delete</button>
    </li>
  </ul>

  <a :href="link">google</a><br />

  <button v-on:click="toggleStatus">change status</button>
</template>