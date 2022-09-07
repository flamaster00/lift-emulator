<script setup>
const props = defineProps({
  floors: Number
})
</script>

<template>

  <div
      class="floorButtonContainer"
      v-for="index in props.floors"
      :key="index"
  >
    <button :key="index">{{index}}</button>
  </div>


</template>

<style>
 .floorButtonContainer {
   padding: 2px;
   width: 40px;
   border-radius: 50%;
   cursor: pointer;
   display: inline-flex;
}
 .floorButtonContainer > button {
   width: 30px;
   height: 30px;
   border-radius: 50%;
   border: 1px solid grey;
 }
</style>