<script>
export default {
  data() {
    return {
      name: "John Doe",
      status: true,
      tasks: ['Task one', 'Task two', 'Task three', 'Task four'],
      link: "https://google.com"
    };
  },
  methods: {
    toggleStatus (){
      if(this.status === 'active'){
        this.status = 'pending'
      } else if (this.status === 'pending'){
        this.status = 'inactive'
      }else{
        this.status = 'active'
      }
    }
  }
};
</script>

<template>
  <h1>Hello {{ name }}</h1>
  <p v-if="status ==='active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is inactive</p>
  <!-- <hr> -->
  <div>
    <ul>
    <li v-for="task in tasks" :key="task">
        {{ task }}
    </li>
  </ul>
  </div>
  <!-- <a v-bind:href="link">Click for Google</a> -->
  <a :href="link">Click for Google</a>
  <br>
  <!-- <button v-on:click="toggleStatus">change status</button> -->
  <button @click="toggleStatus">change status</button>
</template>

<style scoped>
h1 {
  color: red;
}
</style>
