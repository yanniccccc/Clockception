<script setup lang="ts">
import { ref, onMounted } from 'vue'

const props = defineProps<{
  minutes: number
  hours: number
}>()
</script>

<template>
  <div class="clock-container">
    <div
      class="hour"
      :style="{
        transform: `translate(0, -50%) rotate(${(hours / 12) * 360 - 90}deg)`,
        backgroundColor:
          props.hours === 7.5 && props.minutes === 37.5 ? 'var(--secondary)' : 'var(--primary)',
      }"
    ></div>
    <div
      class="minute"
      :style="{
        transform: `translate(0, -50%) rotate(${(minutes / 60) * 360 - 90}deg)`,
        backgroundColor:
          props.hours === 7.5 && props.minutes === 37.5 ? 'var(--secondary)' : 'var(--primary)',
      }"
    ></div>
  </div>
</template>

<style scoped>
.clock-container {
  position: relative;
  width: 100%;
  aspect-ratio: 1 / 1;
  border-radius: 20%;
  border: 1px solid var(--secondary);
  transition: border-color 3s ease;
}

.hour,
.minute {
  height: 8%;
  border-radius: 5px;
  background-color: var(--primary);
  position: absolute;
  top: 50%;
  left: 50%;
  transform-origin: center left;
  transition:
    transform 0.5s ease-out,
    background-color 1s ease;
}
.hour {
  width: 48%;
}
.minute {
  width: 48%;
}
</style>
