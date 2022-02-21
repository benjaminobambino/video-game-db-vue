<template>
  <div class="card" @click="selectGenre(genre.id, genre.name)">
    <div class="image-wrapper">
      <img :src="genre.image_background" :alt="genre.name" />
    </div>
    <div class="info-wrapper flex-col">
      <h3>{{ genre.name }}</h3>
    </div>
  </div>
</template>

<script>
export default {
  name: 'GenreCard',
  props: ['genre'],
  methods: {
    selectGenre() {
      this.$emit('selectGenre', this.genre.id, this.genre.name)
    }
  }
}
</script>
