<script setup>

import {computed, ref, watch} from "vue";

const props = defineProps({
  floorNumber: Number,
})

const emit = defineEmits(['queue'])

const currentFloor = ref(1)
const nextFloor = ref (1)
const queue = ref([])
const isMoving = ref(false)
const isWaiting = ref(false)
const isReady = ref(true)

function checkPressedButton(floor) {
  //  NO items in queue
  if (!queue.value.length) {
    if (floor !== currentFloor.value) {
      queue.value.push(floor)
      emit('queue', queue.value)
    }
  } else {
    // there ARE items in queue
    if (queue.value.indexOf(floor) === -1) {
      queue.value.push(floor)
      emit('queue', queue.value)
    }
  }
}

function liftStart() {
  if (queue.value.length) {
    if (isReady.value) {
      const nextFloor = queue.value[0]
      liftMoving(nextFloor)
      }
  }
}
function liftMoving(floor) {
  isReady.value = false
  isMoving.value = true
  nextFloor.value = floor

}
function liftWaiting() {
  isMoving.value = false
  isWaiting.value = true
  currentFloor.value = nextFloor.value

  setTimeout(() => {
    liftReady()
  }, 3000)
}
function liftReady() {
  queue.value.shift()
  emit('queue', queue.value)
  isWaiting.value = false
  isReady.value = true
}
const moveToFloor = computed(() => {
  const position = -((nextFloor.value - 1) * 100)
  const transition = Math.abs(nextFloor.value - currentFloor.value)
  return `top: ${position}px; transition: top ${transition}s ease-in-out`
})

const direction = computed(() => {
  return nextFloor.value - currentFloor.value
})

// call liftWaiting() after moving transition ended.
// moved this function here because it won't work in liftStart() function after liftMoving()
// as it can't see isWaiting change
function transitionEnd() {
  liftWaiting()
}

// checkPressedButton function can't see new value of props.floorNumber without watcher
watch(
    () => props.floorNumber,
    () => {
      checkPressedButton(props.floorNumber)
      if (isReady.value) {
        liftStart()
      }
    }
)

// Without isReady lift won't start after finishing move to floor
watch(
    () => [queue.value, isReady.value],
    liftStart
)

checkPressedButton(props.floorNumber)

</script>

<template>

  <div
      class="lift"
      :style="moveToFloor"
      :class="{'is-moving': isMoving, 'is-waiting': isWaiting, 'is-ready':isReady}"
      @transitionend="transitionEnd"
  >
    <div class="screen">{{nextFloor}}</div>
    <div>
      <div
          class="arrow-up"
          :class="{up: direction > 0, 'is-waiting-up': isWaiting}"

      >
      </div>
      <div
          class="arrow-down"
          :class="{down: direction < 0, 'is-waiting-down': isWaiting}"
      >
      </div>
    </div>
  </div>

</template>

<style scoped>
.lift {
  height: 100px;
  width: 100px;
  padding-top: 10px;
  position: absolute;
  top: 0;
  left: 0;
  z-index: -1;
  transition: 1s ease-in-out;
  display: flex;
  justify-content: flex-end;
}

.screen {
  width: 30px;
  height: 30px;
  margin-top: 3px;
  border: 1px solid black;
  border-radius: 5px;
  background: linear-gradient(#209cff 0%, #68e0cf 100%);
  display: flex;
  justify-content: center;
  align-items: center;
}

.arrow-up {
  width: 0;
  height: 0;
  margin: 3px 10px;
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;
  border-bottom: 13px solid black;
}

.arrow-down {
  width: 0;
  height: 0;
  margin: 3px 10px;
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;
  border-top: 13px solid black;
}
.up {
  border-bottom: 13px solid red;
}
.down {
  border-top: 13px solid red;
}
.is-waiting-up{
  animation: blink-animation-up 0.7s infinite;
  -webkit-animation: blink-animation-up 0.7s infinite;
}
.is-waiting-down{
  animation: blink-animation-down 0.7s  infinite;
  -webkit-animation: blink-animation-down 0.7s  infinite;
}
@keyframes blink-animation-up {
  to {
    border-bottom: 13px solid red;
  }
}
@-webkit-keyframes blink-animation-up {
  to {
    border-bottom: 13px solid black;
  }
}
@keyframes blink-animation-down {
  to {
    border-top: 13px solid red;
  }
}
@-webkit-keyframes blink-animation-down {
  to {
    border-top: 13px solid black;
  }
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