<script setup>
import TaskList from './TaskList.vue';
import { reactive, ref } from 'vue';
const renderTrigger = ref(0);
const data = ref('')
const current = reactive({
  text: 'all',
})
let todo = reactive({
    taskList: []
})
function addMe() {
  const obj = {
    id: Date.now(),
    task: data.value,
    status: "Incomplete",
  }
  data.value = "";
  todo.taskList.push(obj);
}
function removeMe(){ 

  todo.taskList=todo.taskList.filter((n)=>n.status!='Done');
}

</script>

<template>
  <div class="container">
    <form>
      <div>
        <h2> Add your task </h2>
        <div class="oneLine">
          <input v-model="data" type="text" placeholder="Your Task....">
          <button @click.prevent="addMe"> Add</button><br>
        </div>
        <div v-if="todo.taskList.length > 0 && current.text == 'all'">
          <TaskList :todo="todo.taskList" />
        </div>
        <div v-if="todo.taskList.length > 0 && current.text == 'active'">
          <TaskList :todo="todo.taskList.filter((n) => n.status == 'Incomplete')" />
        </div>
        <div v-if="todo.taskList.length > 0 && current.text == 'completed'">
          <TaskList :todo="todo.taskList.filter((n)=> n.status=='Done')" />
        </div>
        <div class="inLine">
          <div v-if="current.text == 'all'">
            <div style="background-color: blue"><button @click.prevent="current.text = 'all'">All</button></div>
          </div>
          <div v-else>
            <button @click.prevent="current.text = 'all'">All</button>
          </div>
          <div v-if="current.text == 'active'">
            <div style="background-color: blue"><button @click.prevent="current.text = 'active'">Active</button></div>
          </div>
          <div v-else>
            <button @click.prevent="current.text = 'active'">Active</button>
          </div>
          <div v-if="current.text == 'completed'">
            <div style="background-color: blue"><button @click.prevent="current.text = 'completed'"> Completed</button></div>
          </div>
          <div v-else>
            <button @click.prevent="current.text = 'completed'"> Completed</button>
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
}

a{
  margin-left: 20px;
  margin-top: 20px;
}
</style>