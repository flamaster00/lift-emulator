<script setup>
import FloorsPanel from "@/components/FloorsPanel";
import LiftShaft from "@/components/LiftShaft";
import {ref} from "vue";

const floors = ref(5)
const liftOnFloor = ref(3)

function clickHandler(floor) {
  console.log('response from child: ' + floor)
  liftOnFloor.value = floor
  console.log('lift is on floor ' + liftOnFloor.value)
}

</script>

<template>
  <h1 class="main-header">Эмулятор лифта</h1>
  <div class="app">
    <LiftShaft :floors="floors" :lift-on-floor="liftOnFloor"/>
    <FloorsPanel :floors="floors" @response="clickHandler"/>
  </div>
<button
@click="clickHandler">
  press me!
</button>
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
