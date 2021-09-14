<template>
    <!-- STAMPA SINGOLA CARD -->
  <div class="card">
      <div class="poster">
        <img :src="posterPath" :alt="item.title || item.name">
      </div>
      <div class="text-card">
        <div>
          Titolo:<strong>{{ item.title || item.name }}</strong>
        </div>
        <div>
          Titolo Originale: <strong>{{ item.original_title || item.original_name }}</strong>
        </div> 
        <div>
          divngua originale:   
          <img class="original-language" v-if="item.original_language === 'en'" src="@/assets/images/en.png" :alt="item.original_language" /> 
          <img class="original-language" v-if="item.original_language === 'it'" src="@/assets/images/it.png" :alt="item.original_language" />
          <span class="language" v-if="item.original_language != 'en' && item.original_language != 'it'"> {{ item.original_language }} </span>
        </div>
        <div>
          Voto: <i v-for="n in 5" :key="n" :class="n <= voteAverage ? 'fas' : 'far'" class="fa-star"></i>
        </div>
        <div>
          <strong>Trama:</strong> <br> {{ storyline  }}
        </div>
      </div>
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
    // MODIFICA VOTO NUMERICO IN STELLE
    voteAverage() {
      const vote = this.item.vote_average / 2;
      return (Math.ceil(vote));
    },
    // VERIFICA PRESENZA COPERTINA FILM
    posterPath() {
      if(this.item.poster_path) {
        return this.urlImage + this.item.poster_path;
      }
      return 'https://www.altavod.com/assets/images/poster-placeholder.png';
    },
  // VERIFICA PRESENZA TRAMA
    storyline() {
      if(this.item.overview ) return this.item.overview; return '..Trama non disponibile..';
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

.poster img {
    width: 100%;
}

// STAMPA INFORMAZIONI FILM CON HOVER
.card {
  height: 450px;
  width: 300px;
  margin: 30px;
  cursor: pointer;
}

.text-card {
  display: none;
}

.card:hover .text-card {
  display: block;
  height: 450px;
  width: 300px;
  background-color: rgb(51, 51, 51);
  border: 2px solid red;
  color: white;
  text-align: center;
  padding: 8px;
  border-radius: 5px;
  line-height: 1.3rem;
  overflow: auto;
}

.card:hover .poster {
  display: none;
}
 
//  COLORE STELLE
.fa-star {
  color: goldenrod;
}

</style>