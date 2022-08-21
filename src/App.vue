<template>
  <div id="app">
    <MySearchBar @search="searchData" />
    <div class="container">
      <div class="film-container">
        <h3>Film</h3>
        <div class="card-container">
          <TheCard v-for="movie in movies" :key="movie.id" :production="movie" />
        </div>
      </div>
      <div class="serieTv-container">
        <h3>Serie Tv</h3>
        <div class="card-container">
          <TheCard v-for="serie in series" :key="serie.id" :production="serie" />
        </div>
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
  min-height: 100vh;
  padding: 50px;
  display: flex;
  flex-direction: column;
  background-color: gray;
  justify-content: space-around;
}

h3 {
  color: white;
  font-size: 35px;
}

.card-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
}

body {
  margin: 0;
}
</style>
