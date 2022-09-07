<script setup>

import LiftCabin from "@/components/LiftCabin";
import { ref} from "vue";

const props = defineProps({
  floors: Number,
  liftOnFloor: Number
})

</script>

<template>
  <div class="floorShaft">
    <div
        v-for="index in props.floors"
        :key="index"
    >
      <LiftCabin v-if="liftOnFloor === index" />
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