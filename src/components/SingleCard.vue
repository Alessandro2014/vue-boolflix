<template>
  <div>
    <li>
      <img v-if="movie.poster_path" :src="`https://image.tmdb.org/t/p/w342${movie.poster_path}`" alt="poster">
      <img v-else src="../assets/images/placeholder.png" alt="poster">
      </li>
      <li> {{ movie.title || movie.name }}</li>
      <li>{{ movie.original_title || movie.original_name }}</li> 
      <li>Lingua originale:   
        <img class="original-language" v-if="movie.original_language === 'en'" src="@/assets/images/en.png" alt="language" /> 
        <img class="original-language" v-if="movie.original_language === 'it'" src="@/assets/images/it.png" alt="language" />
        <span class="language" v-if="movie.original_language != 'en' && movie.original_language != 'it'"> {{ movie.original_language }} </span>
      </li>
    <li> Voto: {{ movie.vote_average }} </li> 
  </div>
</template>

<script>

export default {
    name: "SingleCard",
    props: ["movie"],
    data() {},
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
  img {
    width: 100%;
  }
}
</style>