<script setup>
import FloorsPanel from "@/components/FloorsPanel";
import LiftShaft from "@/components/LiftShaft";
import {reactive, ref} from "vue";

const floors = ref(8)
const liftCount = ref(4)
const floorPressed = reactive({floor: 1, count: 0})
const queue = ref([])
const lifts = ref([{}])


function sendLiftToFloor(floor) {
  floorPressed.floor = floor
  floorPressed.count++
}

function getLiftsDataArray(liftsData) {
lifts.value = liftsData
}

</script>

<template>
  <h1 class="main-header">Эмулятор лифта</h1>
  <div class="app">
    <LiftShaft
        :floors="floors"
        :floor-pressed="floorPressed"
        :lift-count="liftCount"
        @lifts="getLiftsDataArray"
    />
    <FloorsPanel
        :floors="floors"
        :queue="queue"
        @response="sendLiftToFloor"
    />
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
