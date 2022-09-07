<script setup>
import {ref} from "vue";

const props = defineProps({
  floors: Number,
})

</script>

<template>
  <div class="floorsPanel">
    <h2>Вызов лифта на этаж</h2>
    <div class="floorButtons">
      <div
          class="floorButtonContainer"
          v-for="index in props.floors"
          :key="index"
      >
        <button
            :key="index"
            @click="moveToFloor = index"
        >
          {{index}}
        </button>
      </div>
    </div>
  </div>

</template>

<style>
 .floorsPanel {
   margin: 10px;
   min-width: 100px;
   text-align: center;
   align-self: start;
}
 .floorButtons {
   max-height: 200px;
   border: 1px solid grey;
   margin: 10px;
   padding: 10px;
   display: flex;
   flex-direction: column-reverse;
   flex-wrap: wrap;
   align-self: start;
}
 .floorButtonContainer {
   padding: 2px;
   width: 40px;
   border-radius: 50%;
   display: inline-flex;
 }
 .floorButtonContainer > button {
   width: 30px;
   height: 30px;
   border-radius: 50%;
   border: 1px solid grey;
   cursor: pointer;

 }
</style>