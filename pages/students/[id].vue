<template>
  <div class="mt-5 container">
    <div class="card">
      <div class="card-header">
        <h4>Eit Student
            <NuxtLink class="btn btn-primary float-end" to="/students">Back</NuxtLink>
        </h4>
      </div>

    <div v-if="isSaving">
        <Loading :title="isSavingTitle" />
    </div>
      <div class="card-body" v-else>
        <form @submit.prevent="updateStudent">
          <div class="mb-3">
            <label>Name</label>
            <input type="text" v-model="student.name" class="form-control"/>
            <span class="text-danger" v-if="this.errorList.name">{{ this.errorList.name[0] }}</span>
          </div>
          <div class="mb-3">
            <label>Email</label>
            <input type="text" v-model="student.email" class="form-control"/>
            <span class="text-danger" v-if="this.errorList.email">{{ this.errorList.email[0] }}</span>
          </div>
          <div class="mb-3">
            <label>Phone Number</label>
            <input type="text" v-model="student.phone" class="form-control"/>
            <span class="text-danger" v-if="this.errorList.phone">{{ this.errorList.phone[0] }}</span>
          </div>
          <div class="mb-3">
            <label>Department</label>
            <input type="text" v-model="student.department" class="form-control"/>
            <span class="text-danger" v-if="this.errorList.department">{{ this.errorList.department[0] }}</span>
          </div>
          <div class="mb-3">
            <input type="submit" class="btn btn-primary"/>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

  export default {
    name: "studentEdit",
    data(){
      return{
        studentId : '',
        student: {},
        isSaving: false,
        isSavingTitle: 'Loading',
        errorList: {}
      }
    },

    mounted(){
        this.studentId = this.$route.params.id;

        this.getStudent(this.studentId);
    },

    methods: {

        getStudent(studentId){
            this.isSaving = true;
            axios.get(`http://127.0.0.1:8000/api/students/${studentId}/edit`).then(res=>{
                this.isSaving = false;
                this.student = res.data.student;
            });
        },
        
      updateStudent(){
        this.isSaving = true;
        this.isSavingTitle = 'Updating';

        var myThis  = this;

        axios.put(`http://127.0.0.1:8000/api/students/${this.studentId}/edit`, this.student).then(res => {

          alert(res.data.student);

          this.isSaving = false;
          this.isSavingTitle = 'Loading'; 
          this.errorList  = {}; 
        })
        .catch(function(error){
          if(error.response){
            if(error.response.status==422){
              myThis.errorList = error.response.data.errors;
            }
          }
          myThis.isSaving = false;
        });
      }
    }
  }

</script>

<style>

</style>