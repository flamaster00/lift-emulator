<script setup>
const props = defineProps({
  floors: Number
})
</script>

<template>

<button
    class="floorButton"
    v-for="index in props.floors"
    :key="index"
>
  {{index}}
</button>

</template>

<style>
 .floorButton {
   width: 50px;
   height: 50px;
   border-radius: 50%;
   cursor: pointer;
   margin: 2px;
}
</style>