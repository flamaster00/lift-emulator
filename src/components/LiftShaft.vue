<script setup>

import LiftCabin from "@/components/LiftCabin";
import {reactive, ref, watch} from "vue";

const props = defineProps({
  floors: Number,
  liftCount: Number,
  floorPressed: Object
})

const lifts = ref([])
const liftToFloor = reactive({})

const emit = defineEmits(['lifts'])

watch(
    () => props.floorPressed.count,
    sendLiftToFloor
)


function getLiftData(liftData) {
  if (lifts.value.indexOf(liftData) === -1) {
    lifts.value.push(liftData)
  }
  emit("lifts", lifts)
}

function chooseLift (liftsArr, targetFloor) {

  let sortLifts = liftsArr.slice()
  // Filter by isReady
  if (sortLifts.filter(lift => lift.isReady).length) {
    let isReadyFiltered = sortLifts.filter(lift => lift.isReady)
    //Filter by lift is not on pressed floor
    if (isReadyFiltered.filter(lift => lift.currentFloor !== targetFloor).length) {
      let filteredByFloor = (isReadyFiltered.filter(lift => lift.currentFloor !== targetFloor))
      //sort by closest floor
      filteredByFloor.sort((a, b) => Math.abs(targetFloor - a.currentFloor) - Math.abs(targetFloor - b.currentFloor))
      return liftToFloor.id = filteredByFloor[0].id
    }
  }}

function sendLiftToFloor() {
  liftToFloor.nextFloor = props.floorPressed.floor
  chooseLift(lifts.value, props.floorPressed.floor)
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
  min-width: 100px;
  height: 80%;
  border: 1px solid grey;
  display: flex;
  flex-direction: column-reverse;

}
.floor-shaft > div {
  padding: 0;
  border: 1px solid blue;
  width: 100px;
  height: 100px;
  position: relative;
}

</style>