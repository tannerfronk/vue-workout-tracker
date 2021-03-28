<template>
    <div id="workoutList-table">
    <table>
        <thead>
            <tr>
                <th>Workout</th>
                <th>Date</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="item in items" :key="item.id">
                <td>{{item.workout}}</td>
                <td>{{item.date}}</td>
            </tr>
        </tbody>
    </table>
</div>
</template>

<script>
    export default {
        name: "WorkoutList",
        props: {
            items: Array
        }
    }
</script>

<style scoped>

</style>