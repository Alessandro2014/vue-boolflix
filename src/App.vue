<template>
  <div id="app">
    <header>
      <h1>BOOLFLIX</h1>
      <Search placeholder="Ricerca film..." @search="getResults" />
    </header>
    <main class="container">
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
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

// UTILS
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

// HEADER
header {
  height: 100px;
  background-color: black;
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
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

ul {
  list-style-type: none;
  margin: 20px;
}

</style>
