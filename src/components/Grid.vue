<script setup>

import { ref } from 'vue'
import Card from "./Card.vue"
import Moveable from "vue-moveable";

const props = defineProps(['id', 'active']);
const cards = ref([
  { id: 1 },
  { id: 2 },
  { id: 3 },
  { id: 4 },
  { id: 5 },
  { id: 6 },
]);
const cardsCount = ref(6);
const targetRef = ref(null);


function addCard() {
  cardsCount.value += 1;
  cards.value.push({ id: cardsCount.value });
}

function delCard(idx){
  cards.value.splice(idx, 1);
}

function onDrag(e) {
  e.target.style.transform = e.transform;
}

function selectItem(e) {
  console.log('Grid ' + e.target.className);
  if (e.target.className === 'card grid-item') {
    targetRef.value = e.target;
  } else {
    targetRef.value = null;
  }
}

</script>


<template>
  <div>
    <div class="grid-controls">
      <button class="button-add-card" @click="addCard">+</button>
      <button class="button-del" @click="$emit('del')">x</button>
    </div>
    <div class="grid" @click="selectItem">
      <card v-for="(item, i) in cards" 
        :class="'grid-item'" 
        :key="item.id" 
        @del="delCard(i)"
      />
    </div>
    <Moveable 
      :target = "props.active ? targetRef : null"                      
      :draggable = "true"
      :origin="false"

      :snappable="true"
      :snapThreshold="5"
      :snapDirections="{ top: true, left:true, bottom:true, right:true }"
      :snapContainer="'.grid'"
      :verticalGuidelines="[0, 300, 310, 610, 620]"
      :horizontalGuidelines="[0, 200, 210, 410, 420]"
      :bounds="{ left:0, top:0, right:0, bottom:0, position:'css' }"
      
      @drag = "onDrag"
    />
  </div>
</template>


<style scoped>

.grid {
  display: grid;
  grid-template-columns: auto auto auto;
  background-color: lightblue;
  justify-content: space-evenly;
  gap: 10px;
  min-width: initial;
  min-height: initial;
}

.grid-controls{
  display: flex;
}

.button-add-card{
  border: 1px solid #333;
  display: block;
  background-color: yellow;
  width: 2em;
  height: 2em;
  border-radius: 10%;
}

.button-add-card:hover {
  cursor: pointer;
  background-color: green;
}

</style>