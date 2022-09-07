<script setup>

import {ref} from "vue";
import TestComponent from "@/components/TestComponent";

const text = ref('Hello')
const count = ref(0)
const color = ref('red')

function increment() {
  count.value++
}
function update(e) {
  text.value = e.target.value
}

</script>

<template>
  <input type="text" @input="update">
  <h2 :style="{color}">{{text}}</h2>
  <h2>{{count}}</h2>
  <button @click="increment">Click Me!</button>

  <h2>Below is test component!</h2>
  <TestComponent/>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
