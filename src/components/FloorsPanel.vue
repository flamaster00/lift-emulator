<script setup>


import {ref, watch} from "vue";

const props = defineProps({
  floors: Number,
  liftCount: Number,
  queue: Array
})

const queue = ref([])

const emit = defineEmits(['response'])

function setNextFloor(id) {
  emit('response', id)
}

function checkQueue() {
  queue.value = props.queue
}

watch(
    () => props.queue,
    checkQueue)

</script>

<template>
  <div class="floors-panel">
    <h2>Вызов лифта на этаж</h2>
    <div class="floor-buttons" >
      <div
          class="floor-button-container"
          v-for="floor in props.floors"
          :key="floor"
      >
        <button
            class="floor-btn"
            :key="floor"
            :class="{
              'active': queue.indexOf(floor) !== -1,
              //next floor button is active if there is only 1 lift
              'next': props.liftCount === 1 && queue.indexOf(floor) === 0
            }"
          @click="setNextFloor(floor)"
           
        >
          {{floor}}
        </button>
      </div>
    </div>
  </div>

</template>

<style scoped>
 .floors-panel {
   border: 1px solid grey;
   padding: 5px;
   margin: 0 10px;
   min-width: 100px;
   text-align: center;
   align-self: start;
   display: flex;
   flex-direction: column;
   align-items: center;
}
 .floor-buttons {
   border: 1px solid grey;
   margin: 10px;
   padding: 10px;
   display: flex;
   flex-wrap: wrap;
   flex-direction: column-reverse;
   align-items: center;
 }
 .floor-button-container {
   padding: 2px;
   width: 40px;
   border-radius: 50%;
   display: inline-flex;

 }

 .floor-btn {
   width: 30px;
   height: 30px;
   border-radius: 50%;
   border: 1px solid #343434;
   cursor: pointer;
   user-select: none;
   box-shadow: 0 1px 2px 0 rgba(0,0,0,0.2), 0 2px 3px 0 rgba(0,0,0,0.19);
   background-color: #656565;
   color: #fff;
 }
 .active {
   border: 2px solid #770a0a;
   background-color: #e14848;
   color: #fff;
 }
 .floor-btn:hover {
   border: 2px solid #16D9E3;
   color: #16D9E3;
 }

 .floor-btn:active {
   background-color: #ce6e6e;
   transform: scale(80%) translateY(2px);
   color: white;
 }
 .next {
   background-color: #209cff;
   border: 2px solid #16D9E3;
 }

</style>