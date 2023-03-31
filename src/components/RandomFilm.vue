<script setup>

import { ref, onMounted } from 'vue'

const filmData = ref(null);

async function getRandomoFilm() {
  const response = await fetch('https://api.kinopoisk.dev/v1/movie/random?token=BW522SP-V884BZ4-K07PJAE-9TAGT4Y');
  const data = await response.json();
  filmData.value = data;
}

onMounted(() => {
  getRandomoFilm();
})

</script>


<template>
  <div>
    <div class="container-film" v-if="filmData !== null">
      <button class="button-del" @click="$emit('del')">x</button>
      <img class="poster" :src="filmData.poster['url']" width="200" height="300"/>
      <div class="name">{{ filmData.name }}</div>
      <div class="year">{{ filmData.year }}</div>
      <div class="rating">Рейтинг: {{ filmData.rating['kp'].toFixed(2) }}</div>
    </div>
</div>
</template>


<style>

.container-film{
  color: black;
  text-align: center;
  background-color: sandybrown;
  border: 1px solid #333;
}

.name{
  width: 200px;
  font-weight: bold;
}

</style>
