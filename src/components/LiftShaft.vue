<script setup>

import LiftCabin from "@/components/LiftCabin";

defineProps({
  floors: Number,
  button: Number
})

const emit = defineEmits(['queue'])

function sendQueueToParent(queue) {
  emit('queue', queue)
}

</script>

<template>
  <div class="floor-shaft">
    <div
        v-for="index in floors"
        :key="index"
    >
      <LiftCabin
        v-if="index === 1"
        :floor-number="button"
        @queue="sendQueueToParent"
      />
      {{index}}
    </div>
  </div>
</template>

<style>
.floor-shaft {
  margin-right: 10px;
  min-width: 100px;
  height: 80%;
  border: 1px solid grey;
  display: flex;
  flex-direction: column-reverse;

}
.floor-shaft > div {
  padding: 0;
  border: 1px solid blue;
  width: 100px;
  height: 100px;
  position: relative;
}

</style>