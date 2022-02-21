<template>
  <div>
    <div class="search">
      <form @submit="getSearchResults" v-on:keyup.enter="getSearchResults">
          <input type="text" :value="searchQuery" @input="handleChange">
          <button type="submit">Search</button>
        </form>
      <h2 v-if="searchResults.length">Search Results</h2>
      <section class="search-results container-grid">
        <GameCard v-for="game in searchResults" :key="game.id" :game="game" @selectGame="selectGame" />
      </section>
    </div>

    <div class="genres" v-if="!searched">
      <h2>Genres</h2>
      <section class="container-grid">
        <GenreCard v-for="genre in genres" :key="genre.id" :genre="genre" @selectGenre="selectGenre" />
      </section>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import GenreCard from '../components/GenreCard.vue'
import GameCard from '../components/GameCard.vue'

const API_KEY = process.env.VUE_APP_RAWG_KEY

export default {
  name: 'Home',
  components: {
    GenreCard,
    GameCard
  },
  data: () => ({
    genres: [],
    searchQuery: '',
    searchResults: [],
    searched: false
  }),
  mounted: async function () {
    await this.getGenres()
  },
  methods: {
    async getGenres() {
      const res = await axios.get(`https://api.rawg.io/api/genres?key=${API_KEY}`)
      const sortedRes = res.data.results.sort(function (a, b) {
        if (a.name < b.name) {
          return -1;
        } else if (a.name > b.name) {
          return 1;
        } else {
          return 0;
        }
      })
      this.genres = sortedRes
    },
    async getSearchResults(e) {
      e.preventDefault()
      const res = await axios.get(`https://api.rawg.io/api/games?search=${this.searchQuery}&key=${API_KEY}`)
      this.searchResults = res.data.results
      this.searched = true
      this.searchQuery = ''
    },
    handleChange(event) {
      this.searchQuery = event.target.value
    },
    selectGame(gameId) {
      this.$router.push(`/details/${gameId}`)
    },
    selectGenre(genreId, genreName) {
      this.$router.push(`/games-by-genre/${genreId}/${genreName}`)
    }
  }
}
</script>
