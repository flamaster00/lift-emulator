<script setup>
import {ref, watch} from "vue";
import {minLiftCount, maxLiftCount, minFloorCount, maxFloorCount} from '../config'

const floorCount = ref(5)
const liftCount = ref(1)


const emit = defineEmits(['floor', 'lift'])

watch(
    () => [floorCount.value, liftCount.value],
    () => {
      console.log(maxLiftCount)
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

</script>

<template>
<div class="container">
  <h2>Параметры приложения</h2>
  <div class="parameter-container">
    <h3>Количество этажей</h3>
    <div style="margin-top: 3px">
      <button class="parameter-btn" @click="floorCount--">-</button>
      <div class="parameter-count">{{floorCount}}</div>
      <button class="parameter-btn" @click="floorCount++">+</button>
    </div>
  </div>
  <div class="parameter-container">
    <h3>Количество лифтов</h3>
    <div style="margin-top: 3px">
      <button class="parameter-btn" @click="liftCount--">-</button>
      <div class="parameter-count">{{liftCount}}</div>
      <button class="parameter-btn" @click="liftCount++">+</button>
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

.parameter-btn {
  cursor: pointer;
  height: 25px;
  width: 40px;
  border-radius: 10px;
  vertical-align: center;
  font-size: 1.2rem;
  border: 1px solid grey;
  box-shadow: 0 1px 2px 0 rgba(0,0,0,0.2), 0 2px 3px 0 rgba(0,0,0,0.19);
}
button:active {
  background-color: #2c3880;
  transform: scale(80%);
  color: white;
}

.parameter-count {
  height: 30px;
  line-height: 30px;
  width: 30px;
  text-align: center;
}

</style>