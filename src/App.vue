<script setup>
import FloorsPanel from "@/components/FloorsPanel";
import LiftShaft from "@/components/LiftShaft";
import {reactive, ref} from "vue";
import AppSettings from "@/components/AppSettings";


const floorCount = ref(5)
const liftCount = ref(1)
const floorPressed = reactive({floor: 1, count: 0})
const queue = ref([])


function sendLiftToFloor(floor) {
  //to be able to recognize multiple clicks on the same button from FloorsPanel
  floorPressed.floor = floor
  floorPressed.count++
}

function getFloorCount(value) {
  floorCount.value = value
}

function getLiftCount(value) {
  liftCount.value = value
}

function getQueueData(queueData) {
  queue.value = queueData
}

</script>

<template>
  <h1 class="main-header">Эмулятор лифта</h1>
  <div class="app">
    <LiftShaft
        :floors="floorCount"
        :floor-pressed="floorPressed"
        :lift-count="liftCount"
        @queue-data="getQueueData"
    />
    <FloorsPanel
        :floors="floorCount"
        :lift-count="liftCount"
        :queue="queue"
        @response="sendLiftToFloor"
    />
    <AppSettings
        @floor="getFloorCount"
        @lift="getLiftCount"
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
