<template>
  <div>
    <form @submit.prevent="handleSubmit" class="flex justify-between" method="post">
        <input v-model="name" class="border border-gray-400 outline-none mx-1 rounded-xl w-full px-4" type="text" placeholder="enter new task" required>
        <button type="submit" class="bg-green-600 p-3 rounded-xl">Add</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios'
export default {
   data(){
    return{
      name : ''
    }
   },

    methods : {
     async handleSubmit(){
        try {
         const req = await axios.post( 
          'http://localhost:3000/addtask' ,
           {name : this.name} 
        )

           window.location.href = '/'

        } catch (error) {
          console.log('there was an error ' , error)
        }
      }
    }

}
</script>

<style>

</style>