<script setup>
import { reactive, ref } from "vue";

let task = ref('')
let tasks = reactive([])

const saveTask = () =>{
  tasks.push({id: tasks.length, task: task.value, done: false})
  task.value = '';
}

const deleteTask = (id) => {
  tasks.splice(id, 1).forEach(item => {
    if(item.id > id) item.id--
  })
};

const editTask = (id) => {
  tasks.forEach(taskSelected => {
    if(taskSelected.id == id){
      const promptValue = prompt('edit task')
      taskSelected.task = promptValue
    }
  })
}
</script>

<template>
  <div>
    <input type="text" id="" placeholder="Your Task..." v-model="task" @keyup.enter="saveTask">
    <button @click="saveTask">Save</button>
  </div>

  <ul>
    <li v-for="item in tasks" :key="item.id" :class="controlStyle">
      {{item.task}}
      <button @click="deleteTask(item.id)">Delete</button>
      <button @click="editTask(item.id)">Edit</button>
    </li>
  </ul>
</template>

<style scoped>
</style>
