<template>
    <table class="table table-stripped table-bordered text-center">
        <thead>
            <tr>
                <th>ID</th>
                <th>Name</th>
                <th>City</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="student in students" :key="student.id">
                <td>{{student.id}}</td>
                <td>{{student.name}}</td>
                <td>{{student.city}}</td>
            </tr>
        </tbody>
        <tfoot class="text-center">
            <tr><td colspan="3"><button class="btn btn-primary" @click="addStudent">Add Student</button></td></tr>
        </tfoot>
    </table>
</template>


<script>
import students from './students.js'
export default {
    data(){
        return{
            students: students
        }
    },

    methods:{
        addStudent(){
            let currentId = this.students.length + 1;
            this.students.push({
                id: currentId,
                name: "Azhar",
                city: "Sohag"
            })
        }
    }
}
</script>