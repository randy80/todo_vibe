<template>
  <div class="home">
    <h1>Todo App</h1>
    <p>Welcome to your todo application</p>
    <router-link to="/login">Login</router-link> |
    <router-link to="/dashboard">Dashboard</router-link>
  </div>
</template>

<script setup lang="ts">
// Home view setup
</script>

<style scoped>
.home {
  padding: 20px;
  text-align: center;
}

h1 {
  color: #2c3e50;
}

a {
  color: #42b983;
  text-decoration: none;
  margin: 0 10px;
}

a:hover {
  text-decoration: underline;
}
</style>