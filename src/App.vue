<template>
  <div class="min-h-screen bg-black text-white flex-col flex items-center justify-center">
    <h1 class="text-3xl text-green-400 py-4">Todo App <font-awesome-icon icon="box"></font-awesome-icon></h1>

    <div class="w-3/4 h-fit bg-gray-700 rounded-2xl">
      <div class="py-2 px-5 flex justify-between items-center">
        <p>Tasks</p>
        <button @click="clicked" class="bg-green-400 px-3 py-1 rounded-lg">
          <font-awesome-icon v-if="showed == false" icon="add"></font-awesome-icon>
          <font-awesome-icon v-if="showed == true" icon="minus"></font-awesome-icon>
        </button>
      </div>
      <div class="px-5 py-3 bg-gray-800 rounded-b-2xl">

        <div class="" v-if="showed == false">
           <Tasks />  
        </div>

        <div class="" v-if="showed == true">
          <AddTask />  
        </div> 
         
      </div>
    </div>

  </div>
</template>

<script>
import AddTask from './components/AddTask.vue'
import Tasks from './components/Tasks.vue'


export default {
   components :{
    Tasks,
    AddTask
   },

   data(){
    return{
        showed : false
    }
   },

   methods : {
     clicked(){
      this.showed = !this.showed
     }
   }
}
</script>

<style>

</style>