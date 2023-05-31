<script setup>
import { propsToAttrMap } from '@vue/shared'
import TaskList from './TaskList.vue'
import { reactive, ref,computed } from 'vue'
const allState = ['all','Done', 'Incomplete']
const renderTrigger = ref(0)
const data = ref('')
const current = reactive({
  text: 'all'
})
let todo = reactive({
  taskList: []
})
function addMe() {
  if (data.value == '') return
  const obj = {
    id: Date.now(),
    task: data.value,
    status: 'Incomplete'
  }
  data.value = ''
  todo.taskList.push(obj)
}
function removeMe() {
  todo.taskList = todo.taskList.filter((n) => n.status != 'Done')
}

function deleteFunction(ID) {
  for (const item of todo.taskList) {
    if (item.id == ID) {
      todo.taskList = todo.taskList.filter((i) => i.id != ID)
    }
  }
}

function doneFunction(ID) {
  for (const item of todo.taskList) {
    if (item.id == ID) {
      if (item.status == 'Incomplete') item.status = 'Done'
      else item.status = 'Incomplete'
    }
  }
}
function handleInput(event) {
  this.text = event.target.innerText
};

const currentList = computed(() => {
  return todo.taskList.filter((n)=> n.status!=current.text)
})


</script>

<template>
  <div class="container">
    <form>
      <div>
        <h2>Add your task</h2>
        <div class="oneLine">
          <input v-model="data" type="text" placeholder="Your Task...." />
          <button @click.prevent="addMe">Add</button><br />
        </div>
        <TaskList
          :todo="currentList"
          :Indicator="current.text"
          @deleteThis="deleteFunction"
          @doneThis="doneFunction"
          @editThis="handleInput"
        />
        <div class="inLine">
          <div v-for="state in allState">
            <button
              :style="{ background: current.text == state ? 'blue' : 'black' }"
              @click.prevent="current.text = state"
            >
              {{ state=='Incomplete'? 'DONE': state=='Done'? 'ACTIVE':'ALL' }}
            </button>
          </div>
        </div>
        <a href="" @click.prevent="removeMe">Clear Completed</a>
      </div>
    </form>
  </div>
</template>

<style scoped>
* {
  box-sizing: border-box;
}

input {
  flex: 1;
  padding: 5px;
  margin-right: 20px;
  margin-left: 20px;
}

h2 {
  text-align: center;
  color: black;
}

.container {
  border-radius: 5px;
  width: 100%;
  background-color: #f2f2f2;
}

.oneLine {
  display: flex;
}

.inLine {
  display: flex;
  margin-left: 20px;
}

button {
  padding: 5px 10px;
  margin-right: 20px;
  margin-left: 20px;
  color: white;
  background-color: black;
}

a {
  margin-left: 20px;
  margin-top: 20px;
}
</style>
