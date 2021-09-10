<template>
  <div id="app">
    <header>
      <input type="search" value="" placeholder="Ricerca film">
      <button>Cerca</button>
    </header>
    <main>
      <div>

      </div>
    </main>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: 'App',

  components: {
    
  },
  created() {
    //${query}
    axios.get('https://api.themoviedb.org/3/movie/550?api_key=e5fb8db6d95f138adcc64dfab8283c0c').then((res) => {
      console.log(res);
    });
  }
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
