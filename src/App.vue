<script setup>
import FloorsPanel from "@/components/FloorsPanel";
import LiftShaft from "@/components/LiftShaft";
import {ref} from "vue";

const floors = ref(5)
const currentFloor = ref(1)
const nextFloor = ref (1)
// const queue = ref([1])

function clickHandler(floor) {
  console.log('from child ' + floor)
  nextFloor.value = floor
}

</script>

<template>
  <h1 class="main-header">Эмулятор лифта</h1>
  <div class="app">
    <LiftShaft
        :floors="floors"
        :current-floor="currentFloor"
        :next-floor="nextFloor"
        @onthefloor="(floor) => currentFloor.value = floor"
    />
    <FloorsPanel :floors="floors" @response="clickHandler"/>
  </div>

</template>

<style>
* {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.main-header {
  text-align: center;
}
.app {
  margin: 10px;
  padding: 10px;
  display: flex;
  height: 100%;
  border: 1px solid black;
}
</style>
