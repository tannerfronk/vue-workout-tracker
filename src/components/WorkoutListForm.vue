<template>
<div id="workout-form">
    <form @submit.prevent="handleSubmit">
        <label>Workout</label>
        <input v-model="item.workout" type="text" />
        <label>Weight</label>
        <input v-model="item.weight" type="text" />
        <label>Date</label>
        <input v-model="item.date" type="date" />
        <button>Add Workout</button>
    </form>
</div>
</template>

<script>
    export default {
        name: "WorkoutListForm",
        data() {
            return {
                item: {
                    workout: '',
                    date: '',
                    reps: 10,
                    sets: 5,
                    weight: '',
                }
            }
        },
        methods: {
            handleSubmit(){
                this.$emit('add:item', this.item)
            }
        }
    }
</script>

<style scoped>

</style>