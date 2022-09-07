<script setup>
const props = defineProps({
  floors: Number
})

function floorPressed(id) {
  console.log('clicked number ' + id)
}
</script>

<template>

  <div
      class="floorButtonContainer"
      v-for="index in props.floors"
      :key="index"
  >
    <button
        :key="index"
        @click="floorPressed(index)"
    >
      {{index}}
    </button>
  </div>


</template>

<style>
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