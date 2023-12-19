<template>
  <div class="app">
    <h1>Todo App</h1>
    <div class="input">
      <input type="text" placeholder="Add new todo" v-model="task" @keyup.enter="addToList" />
      <button @click="addToList"></button>
    </div>
    <div class="list">
      <div class="listItem" v-for="(item, index) in tasks" :key="item.id" @click="solveTask(index)" :class="{solved: solvedTasks.includes(index)}">
        <div class="task">
          <h3 v-text="item"/>
        </div>
        <div class="delete" @click.stop="deleteTask(item)"><img src="/delete.svg" alt=""></div>
      </div>
    </div>
    <div class="deleteAll" v-if="tasks.length > 0">
      <p>You have {{ tasks.length }} pending tasks</p>
      <button @click="tasks = []" v-if="tasks.length > 1">
        Delete all tasks
      </button>
    </div>
</div>
</template>

<script setup>
import { ref } from 'vue'

const tasks = ref([])
const task = ref("")
const solvedTasks = ref([])

function addToList() {
  if(task.value) {
    tasks.value.push(task.value)
    task.value = ""
  }
}

function deleteTask(task) {
  let i = tasks.value.indexOf(task)
  tasks.value.splice(i, 1)
  if (solvedTasks.value.includes(i)) {
    solvedTasks.value.splice(solvedTasks.value.indexOf(i), 1)
  }
}

function solveTask(index) {
  if (solvedTasks.value.includes(index)) {
    solvedTasks.value.splice(solvedTasks.value.indexOf(index), 1)
  } else {
    solvedTasks.value.push(index)
  }
}
</script>
