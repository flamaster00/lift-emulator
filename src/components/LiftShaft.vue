<script setup>

import LiftCabin from "@/components/LiftCabin";
import {reactive, ref, watch} from "vue";

const props = defineProps({
  floors: Number,
  liftCount: Number,
  floorPressed: Number
})

const queueData = ref([])
const liftToFloor = reactive({})

const emit = defineEmits(['queue-data'])

watch(
    () => props.floorPressed,
    sendLiftToFloor
)


function getLiftData(liftData) {
  if (queueData.value.indexOf(liftData) === -1) {
    queueData.value.push(liftData)
  }
  let newQueue = []
  queueData.value.forEach(lift => {
    newQueue = [...newQueue, ...lift.queue]
  })
  emit("queue-data", newQueue)
}

function chooseLift (liftsArr, targetFloor) {


  let sortLifts = JSON.parse(JSON.stringify(liftsArr.slice()))
  for (let lift of sortLifts) {
    if ((lift.queue.includes(targetFloor)) || (targetFloor === lift.currentFloor) || (targetFloor === lift.nextFloor)) {
      return liftToFloor.id = null
    }
  }

    sortLifts.sort((a, b) => {
      return ((a.queue.length - b.queue.length) || (Math.abs(a.nextFloor - targetFloor) - Math.abs(b.nextFloor - targetFloor)) )
    })
    return liftToFloor.id = sortLifts[0].id

}

function sendLiftToFloor() {
  liftToFloor.nextFloor = props.floorPressed
  chooseLift(queueData.value, props.floorPressed)
}

</script>

<template>
  <div
      class="floor-shaft"
      v-for="lift in liftCount"
      :key="lift"
  >
    <div
        v-for="floor in floors"
        :key="floor"
    >
      <LiftCabin
        v-if="floor === 1"
        :data="liftToFloor"
        :lift-id="lift"
        @lift="getLiftData"
      />
      {{floor}}
    </div>
  </div>
</template>

<style>
.floor-shaft {
  margin-right: 10px;
  height: 80%;
  border: 1px solid black;
  display: flex;
  flex-direction: column-reverse;
  background-color: #2c3880;
  z-index: -10;
}
.floor-shaft > div {
  padding: 0;
  border: 1px solid grey;
  width: 102px;
  height: 100px;
  position: relative;
  color: #fff;
}

</style>