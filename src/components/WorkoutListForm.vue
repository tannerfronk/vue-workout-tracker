<template>
<div id="workout-form">
    <form @submit.prevent="handleSubmit">
        <label>Workout</label>
        <input v-model="item.workout" type="text" 
        :class="{'has-error' : submitting && invalidWorkout}" 
        @focus="clearStatus" />
        <label>Date</label>
        <input v-model="item.date" type="date"
        :class="{'has-error' : submitting && invalidDate}" 
        @focus="clearStatus" />

        <div class="typeSelection">
            <input type="radio" id="time" name="type" value="time" v-model="picked">
            <label for="time">Time/Distance</label>
            <input type="radio" id="sets" name="type" value="sets" v-model="picked">
            <label for="sets">Sets/Reps/Weight</label>
        </div>
        <div v-if="picked === 'time'">
            <label>Time</label>
            <input v-model="item.time" type="number"
            :class="{'has-error' : submitting && invalidSets}" 
            @focus="clearStatus" />
            <label>Distance</label>
            <input v-model="item.distance" type="text"
            :class="{'has-error' : submitting && invalidSets}" 
            @focus="clearStatus" />
        </div>
        <div v-if="picked === 'sets'">
            <label>Sets</label>
            <input v-model="item.sets" type="number"
            :class="{'has-error' : submitting && invalidSets}" 
            @focus="clearStatus" />
            <label>Reps</label>
            <input v-model="item.reps" type="number"
            :class="{'has-error' : submitting && InvalidReps}" 
            @focus="clearStatus" />
            <label>Weight</label>
            <input v-model="item.weight" type="number"
            :class="{'has-error' : submitting && invalidWeight}" 
            @focus="clearStatus" />
        </div>
        
        <button>Add Workout</button>
        <p v-if="error && submitting" class="error-message">
            Please fill out all required fields
        </p>
        <p v-if="success" class="success-message">Workout successfully added!</p>
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
                    reps: '',
                    sets: '',
                    weight: '',
                    time: '',
                    distance: ''
                },
                submitting: false,
                error: false,
                success: false,
                picked: null
            }
        },
        methods: {
            handleSubmit(){
                this.submitting = true
                this.clearStatus()

                if(this.invalidWorkout || this.invalidWeight || this.invalidDate){
                    this.error = true
                    return
                }

                this.$emit('add:item', this.item)
                this.item = {
                    workout: '',
                    weight: '',
                    date: '',
                }

                this.error = false
                this.success = true
                this.submitting = false
            },
            clearStatus(){
                this.success = false
                this.error = false
            }
        },
        computed: {
            invalidWorkout() {
                return this.item.workout.trim() === ''
            },
            invalidWeight() {
                return this.item.weight.trim() === ''
            },
            invalidDate() {
                return this.item.date === ''
            },
            invalidTime() {
                return this.item.time === ''
            },
            invalidSets() {
                return this.item.sets.trim() === ''
            },
            invalidReps() {
                return this.item.reps.trim() === ''
            },
            invalidDistance() {
                return this.item.distance.trim() === ''
            }
        }
    }
</script>

<style scoped>

form {
    margin-bottom: 2rem;
    text-align: left;
}
form button {
    margin-top: 1rem;
}

[class*='-message'] {
    font-weight: bold;
}

.error-message {
    color: red;
}

.success-message {
    color: green;
}
.typeSelection {
    display: flex;
}
.typeSelection input {
    margin-top: 22px;
    margin-right: 8px;
}
#sets {
    margin-left: 1rem;
}

</style>