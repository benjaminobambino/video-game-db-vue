<template>
  <div class="view-games">
    <h1>Games</h1>
    <section class="dropdown-menu">
      <label for="sort">Sort Games by Rating:</label>
      <br />
      <select name="sort" id="sort" @change="sortGames">
        <option value=""></option>
        <option value="asc">Ascending</option>
        <option value="desc">Descending</option>
      </select>
    </section>
    <div class="container-grid search-results">
      <GameCard v-for="game in games" :key="game.id" :game="game" @selectGame="selectGame" />
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import GameCard from '../components/GameCard.vue'
const API_KEY = process.env.VUE_APP_RAWG_KEY
export default {
  name: 'ViewGames',
  components: {
    GameCard
  },
  data: () => ({
    games: []
  }),
  mounted() {
    this.getGames()
  },
  methods: {
    async getGames() {
      const res = await axios.get(`https://api.rawg.io/api/games?key=${API_KEY}`)
      this.games = res.data.results
    },
    sortGames(e) {
      const sortAsc = () => {
        this.games.sort((a, b) => {
          return a.rating - b.rating
        })
      }
      const sortDesc = () => {
        this.games.sort((a, b) => {
          return b.rating - a.rating
        })
      }
      e.target.value === 'asc' ? sortAsc() : sortDesc()
    },
    selectGame(gameId) {
      this.$router.push(`/details/${gameId}`)
    }
  }
}
</script>
