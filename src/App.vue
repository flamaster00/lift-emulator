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
  queue.value.push(floor)
  console.log(queue.value)
  lift()
}

function lift() {
  if (queue.value.length) {
    if (isReady.value) {
      const nextFloor = queue.value.shift()
      console.log(queue.value)
      liftMoving(nextFloor)
      if (isWaiting.value) {
        liftWaiting(isWaiting.value)
      }
    }
  }
}

watch(
    () => isReady.value,
    lift
)

function liftMoving(floor) {
  console.log('lift is moving to floor ' + floor)
  isReady.value = false
  isMoving.value = true
  nextFloor.value = floor
  console.log('isReady - ' + isReady.value, 'isMoving - ' + isMoving.value, 'isWaiting - ' + isWaiting.value)
}

function liftWaiting(liftWaiting) {
  console.log('I AM WAITING!!!!')
  isMoving.value = !isMoving.value
  isWaiting.value = liftWaiting
  console.log('isReady - ' + isReady.value, ', isMoving - ' + isMoving.value, ', isWaiting - ' + isWaiting.value)
  setTimeout(() => {
    liftReady()
  }, 3000)
}

function liftReady() {
  currentFloor.value = nextFloor.value
  isWaiting.value = !isWaiting.value
  isReady.value = !isReady.value
  console.log('I AM READY!!!')
  console.log('isReady - ' + isReady.value, ', isMoving - ' + isMoving.value, ', isWaiting - ' + isWaiting.value)
  console.log('current floor ' + currentFloor.value + ' and next floor ' + nextFloor.value)
}

const moveToFloor = computed(() => {
  const position = -((nextFloor.value - 1) * 100)
  const transition = Math.abs(nextFloor.value - currentFloor.value)
  console.log(`top: ${position}px; transition: ${transition}s ease-in-out`)
  return `top: ${position}px; transition: top ${transition}s ease-in-out`
})

</script>

<template>
  <h1 class="main-header">Эмулятор лифта</h1>
  <div class="app">
    <LiftShaft
        :floors="floors"
        :moving="moveToFloor"
        @liftstopped="liftWaiting"
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
