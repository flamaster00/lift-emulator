<script setup>

const props = defineProps({
  floors: Number,
  queue: Array
})

const emit = defineEmits(['response'])

function setNextFloor(id) {
  emit('response', id)
}

</script>

<template>
  <div class="floors-panel">
    <h2>Вызов лифта на этаж</h2>
    <div class="floor-buttons">
      <div
          class="floor-button-container"
          v-for="index in props.floors"
          :key="index"
      >
        <button
            :key="index"
            :class="{active: queue.includes(index)}"
            @click="setNextFloor(index)"
        >
          {{index}}
        </button>
      </div>
    </div>
  </div>

</template>

<style>
 .floors-panel {
   border: 1px solid black;
   margin: 10px;
   min-width: 100px;
   text-align: center;
   align-self: start;
}
 .floor-buttons {
   max-height: 200px;
   border: 1px solid grey;
   margin: 10px;
   padding: 10px;
   display: flex;
   flex-direction: column-reverse;
   flex-wrap: wrap;
   align-self: start;

 }
 .floor-button-container {
   padding: 2px;
   width: 40px;
   border-radius: 50%;
   display: inline-flex;

 }
 .floor-button-container > button {
   width: 30px;
   height: 30px;
   border-radius: 50%;
   border: 1px solid grey;
   cursor: pointer;
   box-shadow: 0 1px 2px 0 rgba(0,0,0,0.2), 0 2px 3px 0 rgba(0,0,0,0.19);
 }
 .active {
   border: 2px solid #770a0a;
   background-color: #e14848;
   color: #fff;
 }

 button:active {
   background-color: #ce6e6e;
   transform: scale(80%) translateY(2px);
   color: white;
 }

</style>