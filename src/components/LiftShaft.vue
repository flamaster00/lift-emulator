<script setup>

import LiftCabin from "@/components/LiftCabin";
import {computed} from "vue";

const props = defineProps({
  floors: Number,
  currentFloor: Number,
  nextFloor: Number
})

const moveToFloor = computed(() => {
  const position = `${-(props.nextFloor - props.currentFloor) * 100}px`;
  const transition = `${props.nextFloor - props.currentFloor}s ease-in-out`;
  console.log(props.currentFloor)
  console.log(props.nextFloor)
  console.log(position)
  console.log(transition)
  console.log(`top: ${position}, transition: ${transition}`)
  return `top: ${position}; transition: ${transition}`
})

</script>

<template>
  <div class="floorShaft">
    <div
        v-for="index in props.floors"
        :key="index"
    >
      <LiftCabin
        v-if="index === 1"
        :style="moveToFloor"
      />
      {{index}}
    </div>
  </div>
</template>

<style>
.floorShaft {
  margin-right: 10px;
  min-width: 100px;
  height: 80%;
  border: 1px solid grey;
  display: flex;
  flex-direction: column-reverse;

}
.floorShaft > div {
  padding: 0;
  border: 1px solid blue;
  width: 100px;
  height: 100px;
  position: relative;
}
</style>