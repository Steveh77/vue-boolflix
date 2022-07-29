<template>
  <div id="app">
    <MySearchBar @search="searchMovies" />

    <div>
      <ul v-for="movie in movies" :key="movie.id">
        <li>{{ movie.title }}</li>
        <li>{{ movie.original_title }}</li>
        <li>{{ movie.vote_average }}</li>
        <li>{{ movie.original_language }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
import MySearchBar from "./components/MySearchBar.vue";
import axios from "axios"

export default {
  name: 'App',
  components: {
    MySearchBar
  },
  data() {
    return {
      movies: [],
      api: {
        baseUri: "https://api.themoviedb.org/3",
        key: "ee60758c3a831bd3e6eef24c05e5e7b6",
        language: "it-IT"

      }
    }
  },
  methods: {
    searchMovies(inputText) {
      // chiamare API
      axios.get(`${this.api.baseUri}/search/movie?api_key=${this.api.key}&query=${inputText}&language=${this.language}`).then((res) => {
        this.movies = res.data.results
      })

    }
  },
}

</script>

<style lang="scss">
</style>
