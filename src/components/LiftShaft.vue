<script setup>

import LiftCabin from "@/components/LiftCabin";

const props = defineProps({
  floors: Number,
  moving: String,
  isMoving: Boolean,
  isWaiting: Boolean,
  isReady: Boolean,
  nextFloor: Number,
  direction: Number
})

const emit = defineEmits(['liftstopped'])

function transitionEnd() {
  emit('liftstopped', true)
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
        :style="moving"
        :class="{'is-moving': isMoving, 'is-waiting': isWaiting, 'is-ready': isReady}"
        :next-floor="props.nextFloor"
        :direction="direction"
        :is-waiting="isWaiting"
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
}
.is-ready {
  background-color: greenyellow;
}



</style>