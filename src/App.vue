<script setup>
import FloorsPanel from "@/components/FloorsPanel";
import LiftShaft from "@/components/LiftShaft";
import {computed, ref, watch} from "vue";

const floors = ref(5)
const currentFloor = ref(1)
const nextFloor = ref (1)
const queue = ref([])
const isMoving = ref(false)
const isWaiting = ref(false)
const isReady = ref(true)

function clickHandler(floor) {
  checkPressedButton(floor)
  liftStart()
}

watch(
    () => isReady.value,
    liftStart
)

function checkPressedButton(floor) {
  //  NO items in queue
  if (!queue.value.length) {
    if (floor !== currentFloor.value) {
      queue.value.push(floor)
    }
  } else {
    // there ARE items in queue
    if (queue.value.indexOf(floor) === -1) {
      queue.value.push(floor)
    }
  }
}

function liftStart() {
  if (queue.value.length) {
    if (isReady.value) {
      const nextFloor = queue.value[0]
      liftMoving(nextFloor)
      if (isWaiting.value) {
        liftWaiting(isWaiting.value)
      }
    }
  }
}

function liftMoving(floor) {
  isReady.value = false
  isMoving.value = true
  nextFloor.value = floor
}

function liftWaiting(liftWaiting) {
  currentFloor.value = nextFloor.value
  isMoving.value = !isMoving.value
  isWaiting.value = liftWaiting
  setTimeout(() => {
    liftReady()
  }, 3000)
}

function liftReady() {
  queue.value.shift()
  isWaiting.value = !isWaiting.value
  isReady.value = !isReady.value
}

const moveToFloor = computed(() => {
  const position = -((nextFloor.value - 1) * 100)
  const transition = Math.abs(nextFloor.value - currentFloor.value)
  return `top: ${position}px; transition: top ${transition}s ease-in-out`
})


</script>

<template>
  <h1 class="main-header">Эмулятор лифта</h1>
  <div class="app">
    <LiftShaft
        :floors="floors"
        :moving="moveToFloor"
        :is-moving="isMoving"
        :is-waiting="isWaiting"
        :is-ready="isReady"
        :next-floor="nextFloor"
        :direction="nextFloor - currentFloor"
        @liftstopped="liftWaiting"
    />
    <FloorsPanel
        :floors="floors"
        :queue="queue"
        @response="clickHandler"
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
