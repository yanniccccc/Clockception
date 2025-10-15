<script setup lang="ts">
import { onMounted, ref } from 'vue'
import BigClock from './components/BigClock.vue'
import Dot from './components/Dot.vue'
import colors from './data/colors.json'
import TimerSwitch from './components/TimerSwitch.vue'

type Colors = {
  '--primary': string
  '--secondary': string
  '--background': string
}

const currentHours = ref(0)
const currentMinutes = ref(0)

const isClock = ref(true)
const timerSeconds = ref(0)
const intervalId = ref<number | null>(null)

const currentPalette = ref<Colors>(colors[2] as Colors)

const startTimer = () => {
  timerSeconds.value = 0
  if (intervalId.value) stopTimer()
  intervalId.value = setInterval(() => {
    timerSeconds.value++
  }, 1000)
}

const stopTimer = () => {
  clearInterval(intervalId.value!)
}

onMounted(() => {
  ;(Object.keys(currentPalette.value) as (keyof Colors)[]).forEach((key) => {
    document.documentElement.style.setProperty(key, currentPalette.value[key])
  })

  setInterval(() => {
    const now = new Date()
    currentHours.value = now.getHours()
    currentMinutes.value = now.getMinutes()
  }, 1000)
})
</script>

<template>
  <div class="big-beautiful-container">
    <div class="big-ass-clock">
      <BigClock
        :number="isClock ? Math.floor(currentHours / 10) : Math.floor(timerSeconds / 60 / 10)"
      />
      <BigClock :number="isClock ? currentHours % 10 : Math.floor(timerSeconds / 60) % 10" />
      <div class="dots-container">
        <Dot />
      </div>
      <BigClock
        :number="isClock ? Math.floor(currentMinutes / 10) : Math.floor((timerSeconds % 60) / 10)"
      />
      <BigClock :number="isClock ? currentMinutes % 10 : (timerSeconds % 60) % 10" />
    </div>
    <TimerSwitch
      @update:is-pressed="
        (isPressed: boolean) => {
          isClock = !isPressed
        }
      "
    />
    <div class="button-group" v-if="!isClock">
      <button @click="startTimer">Start</button><button @click="stopTimer">Stop</button>
    </div>
  </div>
</template>

<style scoped>
.button-group {
  display: flex;
  flex-direction: row;
  gap: 5px;
}

.big-ass-clock {
  display: flex;
  width: fit-content;
  height: 30%;
  justify-content: center;
  gap: 8px;
  padding: 8px;
}

.dots-container {
  display: flex;
  flex-direction: column;
  width: fit-content;
  justify-content: center;
  gap: 4px;
}

.big-beautiful-container {
  height: 100dvh;
  width: full;
  display: flex;
  flex-direction: column;
  gap: 40px;
  justify-content: center;
  align-items: center;
}
</style>
