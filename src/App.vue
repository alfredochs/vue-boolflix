<template>
  <div id="app" class="container">
    <div class="input-group mb-3">
      <input
        type="text"
        class="form-control"
        placeholder="Cerca ..."
        aria-label="Recipient's username"
        aria-describedby="button-addon2"
        v-model="query"
        @keyup.enter="printAll()"
      />
      <button
        class="btn btn-outline-secondary"
        type="button"
        id="button-addon2"
        @click="printAll()"
      >
        Button
      </button>
    </div>

    <ul>
      <li v-for="movie in movies" :key="movie.id">
        {{ movie.title }}
        ({{ movie.original_title }}) <br />
        {{ movie.vote_average }}
        {{ movie.original_language }}
        <img
          :src="bandiere[movie.original_language]"
          alt=""
          style="width: 20px"
        />
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
      bandiere: {
        it: "https://upload.wikimedia.org/wikipedia/commons/c/ca/Bandiera_italiana_foto.svg",
        en: "data:image/png;base64,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",
      },
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
    printAll() {
      this.searchQuery("/search/movie", this.query, "movies");
    },
  },
  mounted() {},
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
</style>
