<template>
    <div id="workoutList-table">
        <p v-if="items.length < 1">There are currently no recorded workouts.</p>
        <div v-else class="workoutCards">
            <div class="card" v-for="item in items" :key="item.id">
                <table>
                    <thead>
                        <tr>
                            <th>Workout</th>
                            <th>Date</th>
                            <th v-if="item.time !== '' && item.distance !== '' && item.reps === ''">Time</th>
                            <th v-if="item.time !== '' && item.distance !== '' && item.reps === ''">Distance</th>
                            <th v-if="item.reps !== '' && item.sets !== ''">Sets</th>
                            <th v-if="item.reps !== '' && item.sets !== ''">Reps</th>
                            <th v-if="item.reps !== '' && item.sets !== ''">Weight</th>
                            <th class="actionCol">Actions</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-if="item.reps !== '' && item.sets !== '' && item.weight !== ''">
                            <td v-if="editing === item.id">
                                <input v-model="item.workout" type="text">
                            </td>
                            <td v-else>{{item.workout}}</td>

                            <td v-if="editing === item.id">
                                <input v-model="item.date" type="text">
                            </td>
                            <td v-else>{{item.date}}</td>
                            
                            <td v-if="editing === item.id">
                                <input v-model="item.sets" type="text">
                            </td>
                            <td v-else>{{item.sets}}</td>

                            <td v-if="editing === item.id">
                                <input v-model="item.reps" type="text">
                            </td>
                            <td v-else>{{item.reps}}</td>

                            <td v-if="editing === item.id">
                                <input v-model="item.weight" type="text">
                            </td>
                            <td v-else>{{item.weight}}</td>

                            <td v-if="editing === item.id"  class="right">
                                <button @click="editWorkout(item)">Save</button>
                                <button class="muted-button" @click="cancelEdit(item)">Cancel</button>
                            </td>

                            <td v-else  class="right">
                                <button @click="editMode(item)">Edit</button>
                                <button @click="$emit('delete:item', item.id)">Delete</button>
                            </td>
                        </tr>
                        <tr v-else>
                            <td v-if="editing === item.id">
                                <input v-model="item.workout" type="text">
                            </td>
                            <td v-else>{{item.workout}}</td>

                            <td v-if="editing === item.id">
                                <input v-model="item.date" type="text">
                            </td>
                            <td v-else>{{item.date}}</td>
                            
                            <td v-if="editing === item.id">
                                <input v-model="item.time" type="text">
                            </td>
                            <td v-else>{{item.time}}</td>

                            <td v-if="editing === item.id">
                                <input v-model="item.distance" type="text">
                            </td>
                            <td v-else>{{item.distance}}</td>

                            <td v-if="editing === item.id"  class="right">
                                <button @click="editWorkout(item)">Save</button>
                                <button class="muted-button" @click="cancelEdit(item)">Cancel</button>
                            </td>

                            <td v-else class="right">
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
    margin-left: .5rem;
}
.actionCol {
    text-align: right;
    padding-right: 4.5rem;
}
.right {
    text-align: right;
}
.card {
    border: 16px solid #f0f0f0;
    padding: 2rem;
    margin-bottom: 1rem;
}
</style>