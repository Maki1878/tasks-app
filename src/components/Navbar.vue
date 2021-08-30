<template>
  <nav class="main-nav">
    <router-link :to="{ name: 'Home' }">Tasks</router-link>
    <router-link :to="{ name: 'AddTask' }">Add a new Task</router-link>
  </nav>
</template>

<script>
export default {};
</script>

<style>
.main-nav {
  text-align: center;
  margin: 40px auto;
}
.main-nav a {
  display: inline-block;
  text-decoration: none;
  margin: 0 10px;
  color: rgb(66, 63, 63);
  font-size: 22px;
}
a.router-link-active {
  border-bottom: 3px solid #5cb5f0;
  padding-bottom: 4px;
}
</style>
