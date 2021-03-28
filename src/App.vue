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
          workout: 'Test',
          date: '2021-03-26',
          reps: '10',
          sets: '4',
          weight: '20',
          time: '',
          distance: ''
        },
        {
          workout: 'Test2',
          date: '2021-03-26',
          reps: '',
          sets: '',
          weight: '',
          time: '20s',
          distance: '1 mile'
        },
        {
          workout: 'Test3',
          date: '2021-03-26',
          reps: '10',
          sets: '4',
          weight: '20',
          time: '',
          distance: ''
        }
      ]
    }
  },
  methods: {
    addWorkout(item){
      const previousWorkoutId = this.workoutItems.length > 0
      ? this.workoutItems[this.workoutItems.length -1].id
      : 0
      const newWorkoutId = previousWorkoutId + 1
      const newWorkout = {...item, newWorkoutId}
      this.workoutItems = [...this.workoutItems, newWorkout]
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
