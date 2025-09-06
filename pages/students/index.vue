<template>
  <div class="container mt-5">
    <div class="card">
        <div class="card-header">
        <h4>Student List
            <NuxtLink class="btn btn-primary float-end" to="/students/create">Create</NuxtLink>
        </h4>
    </div>
    <div class="card-body">
        <div v-if="isLoading">
            <Loading title="loading...." />
        </div>
        <div v-else>
            <table class="table table-striped table-bordered">
                <thead>
                    <tr>
                        <td>Serial no</td>
                        <th>Name</th>
                        <th>Email</th>
                        <th>Phone Number</th>
                        <th>Department</th>
                        <th>Action</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(student, index) in students" :key="index">
                        <td>{{ index + 1 }}</td>
                        <td>{{ student.name }}</td>
                        <td>{{ student.email }}</td>
                        <td>{{ student.phone }}</td>
                        <td>{{ student.department }}</td>
                        <td>
                            <NuxtLink class="btn btn-success" :to="`/students/${student.id}`">Edit</NuxtLink>
                            <button class="btn btn-danger" @click="deleteStudent($event, student.id)">Delete</button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios';

    export default{
        name: 'students',
        data(){
            return{
                students: {},
                isLoading: true
            }
        },
        mounted(){
            this.getStudents()
        },
        methods:{
            
            getStudents(){
                this.isLoading = true;
                axios.get(`http://127.0.0.1:8000/api/students`).then(res=>{
                    this.students = res.data.students;
                    this.isLoading = false;
                });
            },
            deleteStudent(event, studentId){
                if(confirm('Are you sure')){
                    event.target.innerText='Deleteing';
                    axios.delete(`http://127.0.0.1:8000/api/students/${studentId}/delete`).then(res=>{
                        event.target.innerText='Delete';
                        this.getStudents();
                    })
                }
            }
        }

    }

</script>

<style>

</style>