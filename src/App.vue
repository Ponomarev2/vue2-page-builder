<script setup>

import { ref } from 'vue'
import Moveable from "vue-moveable"
import Card from './components/Card.vue'
import Grid from './components/Grid.vue'
import RandomFilm from './components/RandomFilm.vue'

const cards = ref([
  { id: 1 },
  { id: 2 },
]);
const grids = ref([
  { id: 101 },
]);
const films = ref([
  { id: 201 },
]);
const cardId = ref(2);
const gridId = ref(101);
const filmId = ref(201);
const targetRef = ref(null);

function addCard() {
  cardId.value += 1;
  cards.value.push({ id: cardId.value });
}

function addGrid() {
  gridId.value += 1;
  grids.value.push({ id: gridId.value });
}

function addFilm() {
  filmId.value += 1;
  films.value.push({ id: filmId.value });
}

function delCard(idx) {
  cards.value.splice(idx, 1);
}

function delGrid(idx) {
  grids.value.splice(idx, 1);
}

function delFilm(idx) {
  films.value.splice(idx, 1);
}

function onDrag(e) {
  e.target.style.transform = e.transform;
}

function selectItem(e) {
  console.log('App ' + e.target.className);
  switch (e.target.className) {
    case 'card card-section':
      targetRef.value = e.target;
      break;
    case 'grid-controls':
    case 'container-film':
      targetRef.value = e.target.parentNode;
      break;
    case 'poster':
    case 'year':
    case 'rating':
    case 'name':
      targetRef.value = e.target.parentNode.parentNode;
      break;
    default:
      targetRef.value = null;
  }
}

</script>

<template>
  <div id="app" @click="selectItem">
    <div class="controls">
      <button @click="addCard">Add Card</button>
      <button @click="addGrid">Add Grid</button>
      <button @click="addFilm">Add Film</button>
    </div>
    <Card v-for="(item, i) in cards" 
      class="card-section" 
      :key="item.id" 
      @del="delCard(i)"
      :style="{ margin: Math.floor(Math.sin(item.id) * 50) + 'px' + ' ' + Math.floor(Math.cos(item.id) * 50) + 'px'}"
    />
    <Grid v-for="(item, i) in grids"
      class="grid-section"
      :key = "item.id"
      :active="targetRef === null"
      @del="delGrid(i)"
    />
    <RandomFilm v-for="(item, i) in films"
      class="film-section"
      :key = "item.id"
      @del="delFilm(i)"
    />
    <Moveable 
      :target = "targetRef"                      
      :draggable = "true"
      :origin="false"
      :snappable="true"
      :bounds="{ left:0, top:0, right:5, bottom:5, position:'css' }"
      @drag = "onDrag"
    /> 
  </div>
</template>


<style scoped>

#app{
  position: initial;
}

.controls{
  position: absolute;
  top:20px;
  left: 20px;
}

.card-section{
  position: absolute;
}

.grid-section{
  position: absolute;
  width: fit-content;
  background-color: gainsboro;
}

.film-section{
  position: absolute;
}

.target {
  position: absolute;
  width: 100px;
  height: 100px;
  top: 150px;
  left: 100px;
  line-height: 100px;
  text-align: center;
  background: #ee8;
  color: #333;
  font-weight: bold;
  border: 1px solid #333;
  box-sizing: border-box;
}

</style>