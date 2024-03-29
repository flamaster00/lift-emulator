<script setup>
import {onBeforeMount, ref, watch} from "vue";
import {minLiftCount, maxLiftCount, minFloorCount, maxFloorCount} from '../config'

const floorCount = ref(5)
const liftCount = ref(1)


const emit = defineEmits(['floor', 'lift'])


//watcher instead of clickHandler functions for increment/decrement each value
watch(
    () => [floorCount.value, liftCount.value],
    () => {
      if (floorCount.value > maxFloorCount) {
        floorCount.value = maxFloorCount
        emit('floor', floorCount.value)
      }
      if (floorCount.value < minFloorCount) {
        floorCount.value = minFloorCount
        emit('floor', floorCount.value)
      }
      if (liftCount.value > maxLiftCount) {
        liftCount.value = maxLiftCount
        emit('lift', liftCount.value)
      }
      if (liftCount.value < minLiftCount) {
        liftCount.value = minLiftCount
        emit('lift', liftCount.value)
      }
        emit('floor', floorCount.value)
        emit('lift', liftCount.value)
      }
)

watch(
    () => [floorCount.value, liftCount.value],
    saveToLS
)

onBeforeMount(() => {
  if (localStorage) {
    const floorCookie = getFromLS('floorCount')
    const liftCookie = getFromLS('liftCount')
    if (floorCookie !== undefined && !Number.isNaN(floorCookie)) {
      floorCount.value = floorCookie
    }
    if (liftCookie !== undefined && !Number.isNaN(liftCookie)) {
      liftCount.value = liftCookie
    }
  }
  
  emit('floor', floorCount.value)
  emit('lift', liftCount.value)
})

function saveToLS() {
  localStorage.setItem("floorCount", String(floorCount.value))
  localStorage.setItem("liftCount", String(liftCount.value))
}

function getFromLS(name) {
  const value = localStorage.getItem(name)
  return Number(value)
}

</script>

<template>
<div class="container">
  <h2>Параметры приложения</h2>
  <div class="parameter-container">
    <h3 style="user-select: none">Количество этажей</h3>
    <div class="count-container">
      <button
          class="parameter-btn"
          @click="floorCount--"
          :disabled="floorCount === minFloorCount"
      >-</button>
      <div class="parameter-count">{{floorCount}}</div>
      <button
          class="parameter-btn"
          @click="floorCount++"
          :disabled="floorCount === maxFloorCount"
      >+</button>
    </div>
  </div>
  <div class="parameter-container">
    <h3 style="user-select: none">Количество лифтов</h3>
    <div class="count-container">
      <button
          class="parameter-btn"
          @click="liftCount--"
          :disabled="liftCount === minLiftCount"
      >-</button>
      <div class="parameter-count">{{liftCount}}</div>
      <button
          class="parameter-btn"
          @click="liftCount++"
          :disabled="liftCount === maxLiftCount"
      >+</button>
    </div>
  </div>
</div>
</template>

<style scoped>

div {
  display: inline-block;
}
.container {
  display: flex;
  flex-direction: column;
  align-self: flex-start;
  align-items: center;
  padding: 10px;
  border: 1px solid grey;
}

.parameter-container {
  margin-top: 5px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.count-container {
  margin-top: 3px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.parameter-btn {
  cursor: pointer;
  user-select: none;
  height: 25px;
  width: 40px;
  border-radius: 10px;
  vertical-align: center;
  font-size: 1.2rem;
  box-shadow: 0 1px 2px 0 rgba(0,0,0,0.2), 0 2px 3px 0 rgba(0,0,0,0.19);
  background-color: transparent;
  border: 2px solid #C0C0C0;
  color: #fff;
}
.parameter-btn:hover:enabled {
  border: 2px solid #16D9E3;
  color: #16D9E3;
}
.parameter-btn:active {
  background-color: #2c3880;
  transform: scale(80%);
  color: white;
}

.parameter-count {
  height: 30px;
  line-height: 30px;
  width: 30px;
  text-align: center;
  user-select: none;
  color: #fff
}

.parameter-btn:disabled {
  background: #ccc;
  border: 2px solid #cc4949;
  cursor: default;
  color: #cc4949;
}

</style>