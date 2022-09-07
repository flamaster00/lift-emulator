<script setup>
import {ref} from "vue";
import FloorButtons from "@/components/FloorButtons";

const floors = ref(5)
</script>

<template>
  <div class="floorsPanel">
    <h2>Вызов лифта на этаж</h2>
    <div class="floorButtons">
      <FloorButtons :floors="floors"/>
    </div>
  </div>

</template>

<style>
 .floorsPanel {
   border: 1px solid grey;
   display: inline-block;
   width: 20%;
   text-align: center;
}
 .floorButtons {
   border: 1px solid grey;
   margin: 10px;
   padding: 10px;
   display: flex;
   justify-content: start;
   flex-wrap: wrap;
}
</style>