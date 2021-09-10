<template>
  <div id="app">
    <header>
      <input type="text" placeholder="Ricerca film"
          v-model.trim="userSearch">
      <button @click="search">Cerca</button>
      <button @click="resetInput">Reset</button>

    </header>
    <main>
      <div v-for="(movie, id) in movies" :key="id">
        <img src="" alt="">
        <h4>{{ movie.title }}</h4>
        <h4>{{ movie.original_title }}</h4> 
        <img class="original-language" v-if="movie.original_language === 'en'" src="@/assets/images/en.png" alt="language" /> 
        <img class="original-language" v-if="movie.original_language === 'it'" src="@/assets/images/it.png" alt="language" /> 

        <h6> {{ movie.vote_average }} </h6> 
      </div>
    </main>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: 'App',
  data() {
    return {
      userSearch: "",
      movies: [],
      baseUri: "https://api.themoviedb.org/3",
      api_key: "e5fb8db6d95f138adcc64dfab8283c0c",
    };
  },
  components: {
  },
  methods: {
    resetInput() {
      this.userSearch = "";
    },
    search() {
      this.getMovies()
      this.resetInput();
    },

    getMovies() {
    const params = {
        params: {
          api_key: this.api_key,
          query: this.userSearch,
          language: "it-IT",
        },
      };

    axios.get(`${this.baseUri}/search/movie`, params).then((res) => {
      this.movies = res.data.results;
    });

    // getLanguage() {
    //   if() {
    //     this.movie.original_language = img
    //   }
    // },
  },
  },
  computed: {},
  
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
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

input, button {
  padding: 5px 20px;
  margin: 0 10px;
}

.original-language {
  height: auto;
  width: 30px;
}


</style>
