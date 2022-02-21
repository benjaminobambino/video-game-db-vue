<template>
  <div class="card game-card" @click="selectGame(game.id)">
    <div class="image-wrapper">
      <img :src="game.background_image" :alt="game.name">
    </div>
    <div class="info-wrapper flex-col">
      <h3>{{ game.name }}</h3>
      <p>{{ game.rating.toFixed(2) }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'GameCard',
  props: ['game'],
  methods: {
    selectGame() {
      this.$emit('selectGame', this.game.id)
    }
  }
}
</script>
