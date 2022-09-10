<script setup>

const props = defineProps({
  nextFloor: Number,
  direction: Number,
  isWaiting: Boolean
})
</script>

<template>

  <div class="lift">
    <div class="screen">{{props.nextFloor}}</div>
    <div>
      <div
          class="arrow-up"
          :class="{up: props.direction > 0, 'is-waiting-up': props.isWaiting}"

      >
      </div>
      <div
          class="arrow-down"
          :class="{down: props.direction < 0, 'is-waiting-down': props.isWaiting}"
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

</style>