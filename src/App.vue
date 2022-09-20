<script setup>
import FloorsPanel from "@/components/FloorsPanel";
import LiftShaft from "@/components/LiftShaft";
import {ref} from "vue";
import AppSettings from "@/components/AppSettings";


const floorCount = ref(null)
const liftCount = ref(null)
const queue = ref([])
const nextFloor = ref(null)


function sendLiftToFloor(floor) {
  nextFloor.value = floor
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
        :floor-pressed="nextFloor"
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
  box-sizing: border-box;
  margin: 0;
}
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  height: 100vh;
  background: linear-gradient(200deg, #29323C 0%, #485563 100%);
  color: #eee;
}
.main-header {
  text-align: center;
}
.app {
  margin: 10px;
  padding: 10px;
  height: 100%;
  display: flex;
  justify-content: flex-start;
}
</style>
