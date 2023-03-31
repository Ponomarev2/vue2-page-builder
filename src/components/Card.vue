<script setup>

import { ref } from 'vue'

const header = ref("Hello World!");
const text = ref("text");

function updateText(e, field) {
  const inputText = e.target.innerText;
  switch (field) {
    case "header":
      this.header = inputText;
      break;
    case "text":
      this.text = inputText;
      break;
    default:
      break;
  }
}

</script>


<template>
  <div class="card" v-once>
    <button class="button-del" @click="$emit('del')">x</button>
    <h2 class="header" contenteditable @input="updateText($event, 'header')">{{header}}</h2>
    <p class="text" contenteditable @input="updateText($event, 'text')">{{text}}</p>
  </div>
</template>


<style>

.card {
  position: relative;
  width: 300px;
  height: 200px;
  background-color: greenyellow;
  justify-content: center;
  border: 1px solid #333;
}

.header {
  color: #000;
  text-align: center;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-weight: bold;
  font-size: larger;
  width: 90%;
  margin-left: 5%;
  background-color: blanchedalmond;
}

.text{
  color: black;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-size: medium;
  text-align: left;
  width: 90%;
  margin-left: 5%;
  height: 65%;
  background-color: seashell;
}

.button-del {
  margin-left: auto; 
  margin-right: 0;
  color: white;
  border: 1px #333;
  display: block;
  background-color: gray;
  width: 2em;
  height: 2em;
  border-radius: 10%;
}

.button-del:hover {
  cursor: pointer;
  background-color: red;
}


</style>