<template>
  <div id="app">
    <header>
      <input type="text" placeholder="Ricerca film"
          v-model.trim="userSearch">
      <button @click="search">Cerca</button>
      <button @click="resetInput">Reset</button>

    </header>
    <main>
      <div v-for="(movie, id) in filteredMovies" :key="id">

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
    search(userText) {
      this.userSearch = userText;
      this.resetInput();
    }
  },
  computed: {
    filteredMovies(){
      return this.movies.filter((movies) => movies.title.includes(this.userSearch));
    }
  },
  created() {
    axios.get(`${this.baseUri}/search/movie?api_key=${this.api_key}&query=${this.userSearch}`).then((res) => {
      this.movies = res.data.results;
      //https://api.themoviedb.org/3/search/movie?api_key=e99307154c6dfb0b4750f6603256716d&query=ritorno+al+futuro
    });
  },
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


</style>
