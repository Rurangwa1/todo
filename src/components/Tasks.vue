<template>
  <div class="font-medium">
    <div class="" v-if="updateForm == false">      
    
           <div class="py-2 flex items-center justify-between" v-for="data in datas" :key="data._id">
        
        <p># {{data.name}}</p>

      <div class="space-x-2">
        <font-awesome-icon @click="update(data._id , data.name)" class="text-green-400 cursor-pointer" icon="edit"></font-awesome-icon>
        <font-awesome-icon @click="deleteTask(data._id)" class="text-green-400 cursor-pointer" icon="trash"></font-awesome-icon>
      </div>
    </div>

      

    </div>


    <div v-else>
    <form @submit.prevent="handleSubmit" class="flex justify-between" method="post">
        <input :value="name" @change="handleChange" class="border border-gray-400 outline-none mx-1 rounded-xl w-full px-4" type="text" placeholder="Update task" required>
        <button type="submit" class="bg-green-600 p-3 rounded-xl cursor-pointer">Update</button>
        <span @click="cancel" class="bg-red-600 flex justify-center items-center cursor-pointer ml-1 p-1 rounded-xl">cancel</span>
    </form>
  </div>


  </div>
</template>

<script>
import axios from 'axios'

export default {
  
  data(){
    return{
      
      datas : null,
      updateForm : false,
      updateId : null,
      deleteId : null,
      name : null
    }
   },

  mounted(){
    this.fetch()
  },

   methods : {

   async handleSubmit(){
       try {
          await axios.post(`http://localhost:3000/update/${this.updateId}` , {name : this.name}) 

          window.location.href = '/'

       } catch (error) {
         console.log('there was an error : ' , error)
       }
   },

    async fetch(){
      
      try {
        const request = await axios.get("http://localhost:3000/")
        const response = request.data.tasks
        this.datas = response
      
      } catch (error) {
        console.log('there is an error : ' , error)
      }

    },

    handleChange(e){
        this.name = e.target.value
    },

   update(id , nam){
     this.updateForm = !this.updateForm
     this.updateId = id
     this.name = nam
   },

   greater(){
     this.datas > 0
   },

   less(){
     this.datas.length < 0
   },

    async deleteTask(id){
       this.deleteId = id
       
       try {
          await axios.get(`http://localhost:3000/delete/${this.deleteId}`)
          window.location.href = '/'
       } catch (error) {
          console.log('there was an error : ' , error)
       }

    },

   cancel(){
      window.location.href = '/'
   }

   },

  
   
}
</script>

<style>

</style>