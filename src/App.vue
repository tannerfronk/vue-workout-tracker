<template>
  <div id="app" class="small-container">
    <h1>Workout Tracker</h1>
    <workout-list-form @add:item="addWorkout" />
    <workout-list :items='workoutItems' @delete:item="deleteWorkout" @edit:item="editWorkout"/>
  </div>
</template>

<script>
import WorkoutList from "./components/WorkoutList";
import WorkoutListForm from "./components/WorkoutListForm";

export default {
  name: 'App',
  components: {
    WorkoutList,
    WorkoutListForm
  },
  data() {
    return {
      workoutItems: [
        {
          id: 1,
          workout: 'Dead-lift',
          date: '2021-03-26',
          reps: '5',
          sets: '4',
          weight: '120',
          time: '',
          distance: ''
        },
        {
          id: 2,
          workout: 'Short Run',
          date: '2021-03-26',
          reps: '',
          sets: '',
          weight: '',
          time: '7 min 12 sec',
          distance: '1.2 miles'
        }
      ]
    }
  },
  methods: {
    addWorkout(item){
      const previousWorkoutId = this.workoutItems.length > 0
      ? this.workoutItems[this.workoutItems.length -1].id
      : 0
      const id = previousWorkoutId + 1
      const newWorkout = {...item, id}
      this.workoutItems = [...this.workoutItems, newWorkout]
      console.log(this.workoutItems)
    },
    deleteWorkout(id){
      this.workoutItems = this.workoutItems.filter(
        item => item.id !== id
        )
    },
    editWorkout(id, updatedItem){
      this.workoutItems = this.workoutItems.map(item =>
      item.id === id ? updatedItem: item
      )
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
