<template>
  <div class="mt-5 container">
    <div class="card">
      <div class="card-header">
        <h4>Create Student</h4>
      </div>
      <div class="card-body">
        <form @submit.prevent="saveStudent">
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
          <div v-if="isSaving">
            <Loading :title="isSavingTitle" />
          </div>
          <div class="mb-3" v-else>
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
    name: "studentCreate",
    data(){
      return{
        student: {
          name: '',
          email: '',
          phone: '',
          department: '',
        },
        isSaving: false,
        isSavingTitle: 'Loading',
        errorList: {}
      }
    },
    methods: {
      saveStudent(){
        this.isSaving = true;
        this.isSavingTitle = 'Saving';

        var myThis = this;

        axios.post(`http://127.0.0.1:8000/api/students`, this.student).then(res => {

          alert(res.data.students);
          
          this.student.name = '';
          this.student.email = '';
          this.student.phone = '';
          this.student.department = '';

          this.isSaving = false;
          this.isSavingTitle = 'Loading';

          this.errorList = {};
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