<script setup>

const props = defineProps({
  floors: Number,
})

const emit = defineEmits(['response'])

function clicked(id) {
  console.log('clicked index is ' + id)
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
            @click="clicked(index)"
        >
          {{index}}
        </button>
      </div>
    </div>
  </div>

</template>

<style>
 .floors-panel {
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

 }
</style>