<script setup>

import {computed, onMounted, reactive, watch} from "vue";

const props = defineProps({
  data: Object,
  liftId: Number,
})

const emit = defineEmits(['lift'])

const lift = reactive({
  id: props.liftId,
  currentFloor: 1,
  nextFloor: 1,
  queue: [],
  isMoving: false,
  isWaiting: false,
  isReady: true
})

onMounted(() => {
  emit('lift', lift)
})

watch(lift,
    () => {
      emit('lift', lift)
})

watch(
    () => props.data.nextFloor,
    () => {
      if (lift.id === props.data.id) lift.queue.push(props.data.nextFloor)
      if (lift.isReady) {
        liftStart()
      }
    }
)

// Without isReady lift won't start after finishing move to floor
watch(
    () => [lift.queue, lift.isReady],
    liftStart
)

function liftStart() {
  if (lift.queue.length) {
    if (lift.isReady) {
      lift.nextFloor = lift.queue[0]
      }
  }
}
function liftMoving() {
  lift.isReady = false
  lift.isMoving = true
}
function liftWaiting() {
  lift.currentFloor = lift.nextFloor
  lift.isMoving = false
  lift.isWaiting = true
  setTimeout(() => {
    liftReady()
  }, 3000)
}
function liftReady() {
  lift.queue.shift()
  lift.isWaiting = false
  lift.isReady = true
}
const moveToFloor = computed(() => {
  const position = -((lift.nextFloor - 1) * 100)
  const transition = Math.abs(lift.nextFloor - lift.currentFloor)
  return `top: ${position}px; transition: top ${transition}s ease-in-out`
})

const direction = computed(() => {
  return lift.nextFloor - lift.currentFloor
})

</script>

<template>

  <div
      class="lift"
      :style="moveToFloor"
      :class="{'is-moving': lift.isMoving, 'is-waiting': lift.isWaiting, 'is-ready':lift.isReady}"
      @transitionstart="liftMoving"
      @transitionend="liftWaiting"
  >
    <div class="screen">{{lift.nextFloor}}</div>
    <div>
      <div
          class="arrow-up"
          :class="{up: direction > 0, 'is-waiting-up': lift.isWaiting}"

      >
      </div>
      <div
          class="arrow-down"
          :class="{down: direction < 0, 'is-waiting-down': lift.isWaiting}"
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