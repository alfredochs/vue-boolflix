<template>
  <div id="app" class="container">
    <div class="input-group input-group-sm mb-3">
      <span class="input-group-text" id="inputGroup-sizing-sm">Small</span>
      <input
        type="text"
        class="form-control"
        aria-label="Sizing example input"
        aria-describedby="inputGroup-sizing-sm"
        v-model="query"
        @keyup.enter="printCards()"
      />
    </div>

    <ul>
      <li v-for="movie in movies" :key="movie.id">
        {{ movie.title }}
        ({{ movie.original_title }}) <br />
        {{ movie.vote_average }}
        ({{ movie.original_language }})
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  components: {},
  data() {
    return {
      apiKey: "f8519d76cebb62a56eaee41d2d683f32",
      apiUrl: "https://api.themoviedb.org/3",
      query: "",
      movies: [],
    };
  },
  methods: {
    searchQuery(url, testoDaCercare, dataKey) {
      axios
        .get(this.apiUrl + url, {
          params: {
            api_key: this.apiKey,
            query: testoDaCercare,
          },
        })
        .then((resp) => {
          this[dataKey] = resp.data.results;
        });
    },
    printCards() {
      this.searchQuery("/search/movie", this.query, "movies");
    },
  },
  mounted() {},
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
</style>
