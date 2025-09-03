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
          </div>
          <div class="mb-3">
            <label>Email</label>
            <input type="text" v-model="student.email" class="form-control"/>
          </div>
          <div class="mb-3">
            <label>Phone Number</label>
            <input type="text" v-model="student.phone" class="form-control"/>
          </div>
          <div class="mb-3">
            <label>Department</label>
            <input type="text" v-model="student.department" class="form-control"/>
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
        isSavingTitle: 'Saving',
      }
    },
    methods: {
      saveStudent(){
        this.isSaving= true,
        this.isSavingTitle= 'Saving'
      }
    }
  }

</script>

<style>

</style>