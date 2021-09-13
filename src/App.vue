<template>
  <div id="app">
    <header>
      <Search placeholder="Ricerca film..." @search="getResults" />
    </header>
    <main class="container">
        <ul v-for="movie in catalogue" :key="movie.id">
          <SingleCard :movie="movie"/>
        </ul>
    </main>
  </div>
</template>

<script>
import axios from "axios";
import Search from '@/components/Search.vue';
import SingleCard from '@/components/SingleCard.vue';
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
    SingleCard,
  },

  computed: {
    catalogue() {
      return [...this.movies, ...this.series];
    }
  },
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
        console.log(res.data.results);
      });
  },
 },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
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
  background-color: chocolate;
  padding: 30px;
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
