<script setup>

const props = defineProps({
  floors: Number
})

</script>

<template>
  <div class="floorShaft">
    <div
        v-for="index in props.floors"
        :key="index"
    >
      {{index}}
    </div>
  </div>

</template>

<style>
.floorShaft {
  width: 10%;
  min-width: 100px;
  height: 80%;
  border: 1px solid grey;
  display: flex;
  flex-direction: column-reverse;

}
.floorShaft > div {
  border: 1px solid blue;
  height: 100px;
}
</style>