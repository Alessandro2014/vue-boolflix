<template>
  <div>
    <li class="cover">
      <img :src="posterPath" :alt="item.title || item.name">
    </li>
    <li>
      Titolo:<strong>{{ item.title || item.name }}</strong>
    </li>
    <li>
      Titolo Originale: <strong>{{ item.original_title || item.original_name }}</strong>
    </li> 
    <li>
      Lingua originale:   
      <img class="original-language" v-if="item.original_language === 'en'" src="@/assets/images/en.png" :alt="item.original_language" /> 
      <img class="original-language" v-if="item.original_language === 'it'" src="@/assets/images/it.png" :alt="item.original_language" />
      <span class="language" v-if="item.original_language != 'en' && item.original_language != 'it'"> {{ item.original_language }} </span>
    </li>
    <li>
      <i v-for="n in 5" :key="n" :class="n <= voteAverage ? 'fas' : 'far'" class="fa-star"></i>
    </li> 
  </div>
</template>

<script>

export default {
    name: "SingleCard",
    props: ["item"],
    data() {
      return {
        urlImage: "https://image.tmdb.org/t/p/w342",
    };
  },
  computed: {
    voteAverage() {
      const vote = this.item.vote_average / 2;
      return (Math.ceil(vote));
    },

    posterPath() {
      if(this.item.poster_path) {
        return this.urlImage + this.item.poster_path;
      }
      return 'https://www.altavod.com/assets/images/poster-placeholder.png';
    },
  },

  
};
</script>

<style scoped lang="scss">
.original-language {
  height: auto;
  max-width: 25px;
  vertical-align: middle;
}

.language {
  text-transform: uppercase;
}

li {
  text-align: center;
  height: auto;
  background-image: url();
  img {
    width: 100%;
  }
}

.fa-star {
  color: goldenrod;
}

</style>