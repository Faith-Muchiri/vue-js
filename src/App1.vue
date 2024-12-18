<script setup>
import { onMounted, ref } from "vue";

// Reactive variables
const name = ref("John Doe");
const status = ref("active");
const tasks = ref(["Task one", "Task two", "Task three", "Task four"]);
const link = ref("https://google.com");
const newTask = ref("");

// Function to toggle status
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
  if(newTask.value.trim() !== '') {
    tasks.value.push(newTask.value);
    newTask.value = '';
  }
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1)
}

onMounted(async () => {
  try{
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
    const data = await response.json();
    tasks.value = data.map((task) => task.title);
  }catch(err){
    console.log(err.message)
  }
})
</script>

<template>
  <!-- Display user name -->
  <h1>Hello {{ name }}</h1>

  <!-- Conditional rendering based on status -->
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is inactive</p>

  <hr />
  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>

  <!-- List of tasks -->
  <div>
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        <span>
          {{ task }}
        </span>
        <button @click="deleteTask(index)">Delete</button>
        </li>
    </ul>
  </div>

  <!-- Dynamic link -->
  <a :href="link" target="_blank">Click for Google</a>
  <br />

  <!-- Button to toggle status -->
  <button @click="toggleStatus">Change Status</button>
</template>

<style scoped>
h1 {
  color: red;
}
button {
  margin-top: 10px;
  padding: 10px;
  background-color: #cea608;
  color: white;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #215759;
}
</style>
