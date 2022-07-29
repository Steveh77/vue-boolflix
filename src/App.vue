<template>
  <div id="app">
    <MySearchBar @search="searchData" />
    <div class="container">
      <div>
        <h3>Film</h3>
        <TheCard v-for="movie in movies" :key="movie.id" :production="movie" />
      </div>
      <div>
        <h3>Serie Tv</h3>
        <TheCard v-for="serie in series" :key="serie.id" :production="serie" />

      </div>
    </div>

  </div>
</template>

<script>
import MySearchBar from "./components/MySearchBar.vue";
import axios from "axios"
import TheCard from "./components/TheCard.vue"

export default {
  name: 'App',
  components: {
    MySearchBar,
    TheCard,
  },
  data() {
    return {
      movies: [],
      series: [],
      api: {
        baseUri: "https://api.themoviedb.org/3",
        key: "ee60758c3a831bd3e6eef24c05e5e7b6",
        language: "it-IT"

      }
    }
  },
  computed: {
    itHadFlag() {
      const flags = ['it', 'en'];
      return flags.includes(this.movies.original_language)
    }
  },
  methods: {
    searchData(inputText) {
      // controllo
      if (!inputText) this.movies = this.series = [];

      // chiamare API
      axios.get(`${this.api.baseUri}/search/movie?api_key=${this.api.key}&query=${inputText}&language=${this.language}`).then((res) => {
        this.movies = res.data.results
      });
      axios.get(`${this.api.baseUri}/search/tv?api_key=${this.api.key}&query=${inputText}&language=${this.language}`).then((res) => {
        this.series = res.data.results
      });
    },
  },
}

</script>

<style lang="scss">
.container {
  display: flex;
  justify-content: space-around;
}
</style>
