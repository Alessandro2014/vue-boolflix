<template>
  <div id="app">
    <header>
      <h1>BOOLFLIX</h1>
      <Search placeholder="Ricerca film..." @search="getResults" />
    </header>
    <main class="container">
      <!-- TRASFERIMENTO INFORMAZIONI AL COMPONENTE CARD -->
      <Main title="Film " id="film" :items="movies"/>
      <Main title="Serie TV " id="series TV" :items="series"/>
    </main>
  </div>
</template>

<script>
import axios from "axios";
import Search from '@/components/Search.vue';
import Main from '@/components/Main.vue';
export default {
  name: 'App',
  data() {
    return {
      movies: [],
      series: [],
      api: {
        baseUri: "https://api.themoviedb.org/3",
        key: "e5fb8db6d95f138adcc64dfab8283c0c",
      },
    };
  },

  components: {
    Search,
    Main,
  },

  computed: {},
  methods: {
    getResults(query) {
        if (!query) {
          this.movies = this.series = [];
          return;
        }
        this.fetchApi(query, 'search/movie', 'movies');
        this.fetchApi(query, 'search/tv', 'series');
      },

    fetchApi(query, endpoint, entity) {
      const params = {
        params: {
          api_key: this.api.key,
          query,
          language: "it-IT",
        },
    };
    axios.get(`${this.api.baseUri}/${endpoint}`, params).then((res) => {
        this[entity] = res.data.results;
      });
  },
 },
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Glory:wght@100&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Glory:wght@100;400;500&display=swap');
#app {
  font-family: 'Glory', sans-serif;
}

// UTILS
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

body {
    background-color: black;
}

// HEADER
header {
  height: 100px;
  background-color: rgb(51, 51, 51);
  padding: 30px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

header h1 {
  font-size: 60px;
  color: red;
}

// MAIN

.container {
  max-width: 1400px;
  margin: 0 auto;
}

.container > div {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
</style>
