<template>
  <div>
    <li>
      <img v-if="movie.poster_path" :src="`https://image.tmdb.org/t/p/w342${movie.poster_path}`" alt="poster">
      <img v-else src="../assets/images/placeholder.png" alt="poster">
      </li>
      <li>Titolo: <strong>{{ movie.title || movie.name }}</strong></li>
      <li>Titolo Originale: <strong>{{ movie.original_title || movie.original_name }}</strong></li> 
      <li>Lingua originale:   
        <img class="original-language" v-if="movie.original_language === 'en'" src="@/assets/images/en.png" alt="language" /> 
        <img class="original-language" v-if="movie.original_language === 'it'" src="@/assets/images/it.png" alt="language" />
        <span class="language" v-if="movie.original_language != 'en' && movie.original_language != 'it'"> {{ movie.original_language }} </span>
      </li>
    <li>
      Voto: <i v-for="(star, index) in voteAverage()" :key="index" class="fas fa-star"></i>
      <i v-for="(star, index) in printFarStars()" :key="index" class="far fa-star"></i>
    </li> 
  </div>
</template>

<script>

export default {
    name: "SingleCard",
    props: ["movie"],
    data() {
      return {
    };
  },
  methods: {
    voteAverage() {
      const vote = this.movie.vote_average / 2;
      return (Math.ceil(vote));
    },
    
    printFarStars() {
      const resultVote = 5 - this.voteAverage();
      return resultVote;
    }
  }

  
};
</script>

<style scoped lang="scss">
.original-language {
  height: auto;
  max-width: 30px;
}

.language {
  text-transform: uppercase;
}

li {
  max-width: 250px;
  height: auto;
  background-image: url();
  img {
    width: 100%;
  }
}
</style>