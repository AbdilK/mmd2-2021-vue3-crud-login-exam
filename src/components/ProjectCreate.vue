<template>
  <div class="card card-body mt-4">
    <!-- using @submit as a click function - add prevent to stop from refreshing page -->
    <form @submit.prevent="onSubmit">    
      <div class="form-group">
        <label>Name</label>
        <input 
          type="text" 
          v-model="form.name" 
          class="form-control" 
          required 
        />
      </div>

      <div class="form-group mt-3">
        <label>Task</label>
        <input 
          type="text"
          class="form-control"
          v-model="form.task"
          required
        />
      </div>

      <button type="submit" class="btn btn-success mt-3">
        Create Project
      </button>
    </form>
  </div>
</template>

<script>
import { reactive } from 'vue'
import { createProject } from '@/firebase.js' // maybe this make error

  export default {
   setup() {
     const form = reactive({
       name: '',
       task: ''
     })

     const onSubmit = async () => {
       // spread operator to add field + invoking our createProject function from firebase.js
       await createProject({ ...form }) 
       // after create - empty input field
       form.name = ''
       form.task = ''
     }

     return { form, onSubmit }
   } 
  }
</script>

<style lang="scss" scoped>

</style>