<script setup>
import FloorsPanel from "@/components/FloorsPanel";
import LiftShaft from "@/components/LiftShaft";
import {ref} from "vue";

const floors = ref(5)
const liftOnFloor = ref(3)



</script>

<template>
  <h1 class="mainHeader">Эмулятор лифта</h1>
  <div class="app">
    <LiftShaft :floors="floors" :lift-on-floor="liftOnFloor"/>
    <FloorsPanel :floors="floors" :lift-on-floor="liftOnFloor"/>
  </div>

</template>

<style>
* {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.mainHeader {
  text-align: center;
}
.app {
  margin: 10px;
  padding: 10px;
  display: flex;
  height: 100%;
  border: 1px solid black;
}
</style>
