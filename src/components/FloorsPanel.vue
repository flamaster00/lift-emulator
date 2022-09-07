<script setup>
import FloorButtons from "@/components/FloorButtons";

const props = defineProps({
  floors: Number
})
</script>

<template>
  <div class="floorsPanel">
    <h2>Вызов лифта на этаж</h2>
    <div class="floorButtons">
      <FloorButtons :floors="props.floors"/>
    </div>
  </div>

</template>

<style>
 .floorsPanel {
   margin: 10px;
   border: 1px solid grey;
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
</style>