<script setup>
import { watch, ref } from 'vue'
const checkboxValue = ref(false)
const props = defineProps({
  todo: Array
})
function handleCheckboxChange(item) {
  if (item.status == 'Incomplete') item.status = 'Done'
  else item.status = 'Incomplete'
}
function handleInput(event) {
      this.text = event.target.innerText;
    }
</script>

<template>
  <div class="black">
    <ul>
      <li v-for="item in props.todo" :key="item.id">
        <div v-if="item.status == 'Incomplete'">
          <input type="checkbox" @change="handleCheckboxChange(item)" />
          <p contenteditable="true" @input="handleInput"> {{ item.task }} </p>
        </div>
        <div v-else>
          <div class="strike">{{ item.task }}</div>
        </div>
        <button class="on-right" @click="props.todo.splice(props.todo.indexOf(item), 1)">
          Delete
        </button>
      </li>
    </ul>
  </div>
</template>

<style scoped>
ul {
  list-style-type: none;
  padding: 0;
}
li{
  display: flex;
}
.black {
  display: flex;
  color: black;
  margin-left: 20px;
  font-size: larger;
}

.list-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #ccc;
}

.on-right {
  margin-left: 10px;
}

.strike {
  text-decoration: line-through;
  position: relative;
}

.strike::after {
  content: '';
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  height: 2px;
  background-color: #000;
}
</style>
