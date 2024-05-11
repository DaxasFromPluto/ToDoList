<script setup>
import { ref } from 'vue'


/* Vytvářím proměnné */
const newTask = ref('')
let id = 0
const tasks = ref([])

/* Sekce funkcí */

function removeTask(task) {
  tasks.value = tasks.value.filter((t) => t !== task)
}
function addTask() {
  tasks.value.push({ id: id++, text: newTask.value, completed:false})
  newTask.value = ''
}
function doneTask(task){
  task.color = 'green';
  task.completed = true
}
function getObjectLength(tasks) {
    let count = 0;
    for (let task in tasks) {
      if (task.hasOwnProperty(key) && task.completed=='true') {
        count++;
      }
    }
    return count;
  }

function remainingTasks(tasks){
  return Object.values(tasks).filter(task => task.completed == false).length
}


</script>

<template>

<h1 class="header">Seznam Úkolů</h1>
<h2 class="secondHeader">Zbývá úkolů: {{ remainingTasks(tasks) }}</h2>
<div class="content">
  <form @submit.prevent="addTask">
    <input v-model="newTask" required placeholder="přidat úkol">
    <button class="Button">Přidat úkol</button>
  </form>
  <div class = "li">
    <ul class="list">
    <li v-for="task in tasks" :key="task.id" class="elements" :style="{ backgroundColor: task.color || 'coral' }">
      {{ task.text }}
      <button class="Button" @click="removeTask(task)">X</button>
      <button class="Button" @click="doneTask(task)">✔</button>
    </li>
  </ul>
  </div>

</div>
  
</template>

<style scoped>
/* Zde styluji moji aplikaci*/
.li{
  display: flex;
  justify-content: center;
}
.Button{
  background-color:black;
  color: white;
  border: none;
}
.Button:hover{
  background-color: green;
}

.header{
  font-size: 3rem;
  font-weight: bold;
  text-align: center;
  color: coral;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
  margin-bottom: 2rem;

}
.content{
  display: grid;
  grid-template-columns: 5;
  text-align: center;

}
.list{
  list-style: none;
  padding: 0;
  margin: 0;
  width: 100%;
  max-width: 500px;
  background-color:coral;
  border-radius: 4px;
}

.secondHeader{
  font-size: 2rem;
  font-weight: normal;
  text-align: center;
  color:coral;
  margin-bottom: 2rem;
}
.elements{
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 12px;
  border-bottom: 2px solid white;
  border-top: 2px solid white


}


</style>
