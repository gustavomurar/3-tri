<script setup>
    import { ref, onMounted } from 'vue';
  import api from '../plugins/axios';

  const moviesGenres = ref([]);
  const TVGenres = ref([]);

  onMounted(async () => {
    let response = await api.get('genre/movie/list?language=pt-BR');
    moviesGenres.value = response.data.genres;
    response = await api.get('genre/tv/list?language=pt-BR');
    TVGenres.value = response.data.genres;
  });
</script>

<template>
    <div>
    <nav>
      <router-link to="/">Home</router-link>
      <router-link to="/filmes">Filmes</router-link>
      <router-link to="/tv">Programas de TV</router-link>
    </nav>
    <router-view />
  </div>
  <h1>Gêneros de filmes</h1>
  <ul>
    <li v-for="genre in moviesGenres" :key="genre.id">
      {{ genre.name }} 
    </li>
  </ul>
  <hr />
  <h1>Gêneros de programas de TV</h1>
  <ul>
    <li v-for="genre in TVGenres" :key="genre.id">
      {{ genre.name }}
    </li>
  </ul>
</template>
<style scoped>
  nav {
    display: flex;
    justify-content: flex-start;
    margin-bottom: 1rem;
    column-gap: 2rem;
  }
</style>