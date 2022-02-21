<template>
  <div class="game-content" v-if="gameDetails">
    <h1>{{ gameDetails.name }}</h1>
    <section class="image-container">
      <div>
        <img :src="gameDetails.background_image" :alt="gameDetails.name" />
      </div>
    </section>
    <section class="details">
      <div class="flex-row space"></div>
      <div>
        <h4 class="rating">Rating: {{ gameDetails.rating.toFixed(2) }}</h4>
        <div v-html="gameDetails.description"></div>
        <div class="details-row">
          <section>
            <h4>Platforms:</h4>
            <p v-for="platform in gameDetails.platforms" :key="platform.platform.id">{{ platform.platform.name }}</p>
          </section>
          <section>
            <h4>Developers:</h4>
            <p v-for="developer in gameDetails.developers" :key="developer.id">{{ developer.name }}</p>
          </section>
          <section>
            <h4 v-if="gameDetails.genres.length > 1">Genres:</h4>
            <h4 v-else>Genre:</h4>
            <p class="clickable" v-for="genre in gameDetails.genres" :key="genre.id" @click="selectGenre(genre.id, genre.name)">{{ genre.name }}</p>
          </section>
          <h4><a :href="gameDetails.website" target="_blank" rel="noopener noreferrer">Vist {{ gameDetails.name }}&#8217;s Website</a></h4>
        </div>
      </div>
    </section>
    <section class="buttons">
      <button @click="goBack">Home</button>
    </section>
  </div>
</template>

<script>
import axios from 'axios'
const API_KEY=process.env.VUE_APP_RAWG_KEY
export default {
  name: 'GameDetails',
  data: () => ({
    gameDetails: null
  }),
  mounted() {
    this.getGameDetails()
  },
  methods: {
    async getGameDetails() {
      const gameId = parseInt(this.$route.params.game_id)
      const res = await axios.get(`https://api.rawg.io/api/games/${gameId}?key=${API_KEY}`)
      this.gameDetails = res.data
    },
    goBack() {
      this.$router.push('/')
    },
    selectGenre(genreId, genreName) {
      this.$router.push(`/games-by-genre/${genreId}/${genreName}`)
    }
  }
}
</script>
