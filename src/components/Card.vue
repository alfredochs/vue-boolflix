<template>
  <div class="">
    <!-- cards bootstrap -->
    <div class="card border-0 h-100" style="width: 18rem">
      <img class="card-img-top h-100" :src="generaImg" alt="Card image cap" />

      <div class="card-body position-absolute h-100 w-100 overlay">
        <h5 class="card-title">{{ generaTitolo }}</h5>
        <div class="card-title" v-if="titoloOriginale">
          <strong>Titolo Originale: </strong>{{ titoloOriginale }}
        </div>
        <p class="card-text" v-if="type.overview">
          <strong>Descrizione: </strong>
          {{ type.overview }}
        </p>
        <ul class="list-group list-group-flush">
          <li class="list-unstyled">
            <i
              class="fa"
              aria-hidden="true"
              v-for="i in 5"
              :key="i"
              :class="arrotondaVoto >= i ? 'fa-star' : 'fa-star-o'"
              style="color: #f5c042"
            >
            </i>
          </li>
        </ul>
      </div>
    </div>
    <!-- fine card bootstrap -->

    <!-- <li class="d-flex flex-column justify-content-center">
      <img :src="generaImg" alt="" class="w-25" />
      <div class="d-none">
        <span v-if="type.overview">Descrizione: </span>
        <p>{{ type.overview }}</p>

        <span>Titolo: {{ generaTitolo }}</span> <br />

        <div v-if="titoloOriginale">
          Titolo Originale: {{ titoloOriginale }}
        </div>
        <br />

        <img :src="generaBandiera" alt="" style="width: 20px" /> -->

    <!-- <div class="d-flex">
          {{ arrotondaVoto }}
        </div> -->
    <!-- 
        <i
          class="fa"
          aria-hidden="true"
          v-for="i in 5"
          :key="i"
          :class="arrotondaVoto >= i ? 'fa-star' : 'fa-star-o'"
        >
        </i>
      </div>
    </li> -->
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    type: Object,
  },

  data() {
    return {
      bandiere: {
        it: "https://upload.wikimedia.org/wikipedia/commons/c/ca/Bandiera_italiana_foto.svg",
        en: "https://www.novalibandiere.it/wp-content/uploads/Gran-bretagna.jpg",
        es: "data:image/png;base64,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",
      },
    };
  },
  computed: {
    generaImg() {
      const apiUrl = "https://image.tmdb.org/t/p/";
      const imgSize = "w342";
      if (!this.type.poster_path) {
        return require("@/assets/unknown.png");
      }
      return apiUrl + imgSize + this.type.poster_path;
    },
    generaBandiera() {
      return this.bandiere[this.type.original_language];
    },
    arrotondaVoto() {
      return Math.ceil(this.type.vote_average / 2);
    },
    generaTitolo() {
      const risultato = this.type.title ? this.type.title : this.type.name;
      return risultato;
    },
    titoloOriginale() {
      const nomeOriginale = this.type.original_title
        ? this.type.original_title
        : this.type.original_name;

      return this.generaTitolo === nomeOriginale ? "" : nomeOriginale;
    },
  },
};
</script>

<style>
@import "../styles/card.scss";
</style>