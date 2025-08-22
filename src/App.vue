<script setup lang="ts">
import { ref } from 'vue';

const count = ref(0);
const moviename = ref('')
const movieduration = ref(0)
const movies = ref([
  {
    name:'Matrix',
    duration: 320
  },
  {
    name:'Lilo & Stitch',
    duration: 190
  },
  {
    name:'Titanic',
    duration: 120
  }
])

const increment = () => {
  count.value++
}
const decrement = () => {
  count.value--
}

const deleteMovie = (movie : {name: string, duration: number}) => {
  movies.value = movies.value.filter((m) => m.name != movie.name)
}

const sortMovies = () => {
  movies.value.sort((a,b) => a.duration > b.duration ? 1 : -1)
}

const handleAddMovie = () => {
  movies.value.push({name: moviename.value, duration: movieduration.value})
  moviename.value = ''
  movieduration.value = 0
}
</script>

<template>
  <p :id="`p-${count}`">Compteur : {{ count }}</p>
  <button @click="increment">Ajouter</button>
  <button @click="decrement">Enlever</button>
  <hr>
  <button @click="sortMovies">Réorganiser</button>
  <form @submit.prevent="handleAddMovie">
    <input v-model="moviename" type="text" name="movie" id="moviename" placeholder="Nom du film">
    <input v-model="movieduration" type="text" name="duration" id="movieduration" placeholder="Durée du film en minutes">

    <button type="submit">Ajouter</button>
  </form>
  <ul>
    <li v-for="movie in movies" :key="movie.name">
      Nom : {{ movie.name }} dure {{ Math.floor(movie.duration / 60) }}h
      <button @click="deleteMovie(movie)">Supprimer</button>
    </li>
  </ul>
</template>

<style scoped></style>
