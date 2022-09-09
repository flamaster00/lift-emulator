<script setup>

import LiftCabin from "@/components/LiftCabin";

import {ref} from "vue";

const props = defineProps({
  floors: Number,

  moving: String
})

const isOnFloor = ref(true)

const emit = defineEmits(['liftstopped'])

function transitionStart() {
  isOnFloor.value = !isOnFloor.value
  console.log('TRANSITION STARTED!!!')
  console.log(isOnFloor.value)

}

function transitionEnd() {
  console.log('TRANSITION ENDED!!!')
  isOnFloor.value = !isOnFloor.value
  console.log(isOnFloor.value)
  emit('liftstopped', true)
}

</script>

<template>
  <div class="floor-shaft">
    <div
        v-for="index in props.floors"
        :key="index"
    >
      <LiftCabin
        v-if="index === 1"
        :style="moving"
        @transitionstart="transitionStart"
        @transitionend="transitionEnd"
      />
      {{index}}
    </div>
  </div>
</template>

<style scoped>
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
.is-moving {
  background-color: aqua;
}
.is-waiting {
  background-color: yellow;
  animation: blink-animation 1s steps(5, start) infinite;
  -webkit-animation: blink-animation 1s steps(5, start) infinite;
}
@keyframes blink-animation {
  to {
    visibility: hidden;
  }
}
@-webkit-keyframes blink-animation {
  to {
    visibility: hidden;
  }
}

.is-ready {
  background-color: green;
}


</style>