<script setup>
let  props = defineProps({
  todo: Array,
  Indicator: String
})
</script>

<template>
  <div class="black">
    <ul>
      <li v-for="item in props.todo.filter((n)=> n.status != Indicator)" :key="item.id">
        <div v-if="item.status == 'Incomplete'">
          <span contenteditable="true" @input="handleInput"> {{ item.task }} </span>
        </div>
        <div v-else>
          <div class="strike">{{ item.task }}</div>
        </div>
        <button class="on-left" @click.prevent="$emit('doneThis',item.id)">
          Done
        </button>
        <button class="on-right" @click.prevent="$emit('deleteThis',item.id)">
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
li {
  display: flex;
  margin-top: 20px;
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
  background-color: red;
}

.on-left {
  margin-left: 10px;
  background-color: greenyellow;
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
