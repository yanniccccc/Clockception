<script setup lang="ts">
import { onMounted, ref } from 'vue'

import SimpleClock from './SimpleClock.vue'
import numbers from '../data/numbers.json'

const props = defineProps<{
  number: number
}>()
</script>

<template>
  <div class="big-clock-container">
    <SimpleClock :hours="time.hour" :minutes="time.minute" v-for="time in numbers[number]" />
  </div>
</template>

<style scoped>
.big-clock-container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  width: fit-content;
  height: 100%;
  gap: 4px;
}
</style>
