<script setup lang="ts">
import { ref } from 'vue';

const addtask = ref('')
const showCompleted = ref(true)
const todolist = ref([
  {
    title: "Tache 1",
    completed: false,
    date: new Date()
  },
  {
    title: "Tache 2",
    completed: false,
    date: new Date()
  },
  {
    title: "Tache 3",
    completed: false,
    date: new Date()
  }
])

const sortList = () => {
  todolist.value = todolist.value.sort((a,b) => (a.completed === b.completed)? 0 : b.completed? -1 : 1)
}

const handleSubmit = () => {
  todolist.value.push({
    title: addtask.value,
    completed: false,
    date: new Date()
  })
  addtask.value = ""
  sortList()
}
</script>

<template>
  <h1>Todolist VueJS Grafikart</h1>
  <form @submit.prevent="handleSubmit">
    <input v-model="addtask" type="text" name="addtask" id="addtask">
    <button type="submit">Ajouter</button>
  </form>

  <h2>Tâches</h2>
  <ul v-if="todolist.length">
    <template v-for="todo in todolist" :key="`todo-${todo.date}-${todo.title}`">
      <li v-if="todo.completed == false || todo.completed && showCompleted">
        <input @change="sortList" v-model="todo.completed" type="checkbox" :name="`todo-${todo.date}-${todo.title}`" :id="`todo-${todo.date}-${todo.title}`">
        <label :for="`todo-${todo.date}-${todo.title}`" :style="{textDecoration: todo.completed ? 'line-through' : ''}">{{ todo.title }}</label>
        <button @click="todolist = todolist.filter((t) => t != todo)">Supprimer</button>
      </li>
    </template>
  </ul>
  <p v-else>Vous n'avez aucune tâche en cours</p>
  <input v-model="showCompleted" type="checkbox" id="toggleDoneTodo"/>
  <label  for="toggleDoneTodo">Voir les tâches complétées</label>
</template>

<style scoped></style>
