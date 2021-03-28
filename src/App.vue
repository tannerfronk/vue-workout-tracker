<template>
  <div id="app" class="small-container">
    <h1>Workout Tracker</h1>
    <workout-list :items='workoutItems' />
  </div>
</template>

<script>
import WorkoutList from "./components/WorkoutList";

export default {
  name: 'App',
  components: {
    WorkoutList
  },
  data() {
    return {
      workoutItems: [
        {
          id: 1,
          workout: 'Arms',
          reps: 10,
          sets: 2,
          weight: 50,
          date: '03/28/21'
        },
        {
          id: 2,
          workout: 'Legs',
          reps: 10,
          sets: 2,
          weight: 100,
          date: '03/28/21'
        },
        {
          id: 2,
          workout: 'Pushups',
          reps: 10,
          sets: 5,
          weight: null,
          date: '03/28/21'
        }
      ]
    }
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
