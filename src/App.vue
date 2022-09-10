<script setup>
import FloorsPanel from "@/components/FloorsPanel";
import LiftShaft from "@/components/LiftShaft";
import { ref } from "vue";

const floors = ref(5)
const floorPressed = ref(1)
const queue = ref([])


function sendLiftToFloor(floor) {
  floorPressed.value = floor
}

function sendQueueToPanel(que) {
  queue.value = que
}

</script>

<template>
  <h1 class="main-header">Эмулятор лифта</h1>
  <div class="app">
    <LiftShaft
        :floors="floors"
        :button="floorPressed"
        @queue="sendQueueToPanel"
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
