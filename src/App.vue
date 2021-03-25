<template>
  <div id="app">
    <WorkoutList />
  </div>
</template>

<script>
import WorkoutList from "./components/WorkoutList";

export default {
  name: 'App',
  components: {
    WorkoutList
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
