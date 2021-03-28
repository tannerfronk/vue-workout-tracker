<template>
    <div id="workoutList-table">
        <p v-if="items.length < 1">There are currently no recorded workouts.</p>
        <div v-else class="workoutCards">
            <div class="card" v-for="item in items" :key="item.id">

                <!-- <h2>Workout: </h2>
                    <h2 v-if="editing === item.id">
                        <input v-model="item.workout" type="text">
                    </h2>
                    <h2 v-else>{{item.workout}}</h2>
                    <h3>Date:</h3> -->
                <table>
                    <thead>
                        <tr>
                            <th>Workout</th>
                            <th>Date</th>
                            <th>Weight</th>
                            <th>Actions</th>
                        </tr>
                    </thead>
                    <tbody>
                        <!-- <tr v-for="item in items" :key="item.id"> -->
                            <tr>
                            <td v-if="editing === item.id">
                                <input v-model="item.workout" type="text">
                            </td>
                            <td v-else>{{item.workout}}</td>

                            <td v-if="editing === item.id">
                                <input v-model="item.date" type="text">
                            </td>
                            <td v-else>{{item.date}}</td>

                            <td v-if="editing === item.id">
                                <input v-model="item.weight" type="text">
                            </td>
                            <td v-else>{{item.weight}}</td>
                            <td v-if="editing === item.id">
                                <button @click="editWorkout(item)">Save</button>
                                <button class="muted-button" @click="cancelEdit(item)">Cancel</button>
                            </td>

                            <td v-else>
                                <button @click="editMode(item)">Edit</button>
                                <button @click="$emit('delete:item', item.id)">Delete</button>
                            </td>
                        </tr>
                    </tbody>
                </table>

            </div>

        </div>

        
    </div>
</template>

<script>
    export default {
        name: "WorkoutList",
        props: {
            items: Array
        },
        data() {
            return {
                editing: null,
                cachedItem: null
            }
        },
        methods: {
            editMode(item){
                this.editing = item.id;
                this.cachedItem = Object.assign({}, item)
            },
            editWorkout(item){
                if(item.workout === '' || item.date === 'blank') return

                this.$emit('edit:item', item.id, item)
                this.editing = null
            },
            cancelEdit(item){
                Object.assign(item, this.cachedItem)
                this.editing = null
            }
        }
    }
</script>

<style scoped>

button {
    margin-right: 1rem;
}

</style>