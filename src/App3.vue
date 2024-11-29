<script>
import { ref } from "vue";

export default {
  setup() {
    const name = ref("ahamd");
    const status = ref("active");
    const tasks = ref(["task 1", "task 2", "task 3"]);
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
    return { name, status, tasks, link, toggleStatus };
  },
};
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">user is active</p>
  <p v-else-if="status === 'pending'">user is pending</p>
  <p v-else>user is inactive</p>

  <h3>Tasks</h3>
  <ul>
    <li v-for="task in tasks" :key="task">
      {{ task }}
    </li>
  </ul>

  <a :href="link">google</a><br />

  <button v-on:click="toggleStatus">change status</button>
</template>