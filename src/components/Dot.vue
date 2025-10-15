<script setup lang="ts">
import SimpleClock from './SimpleClock.vue'
</script>

<template>
  <div class="dot-container">
    <SimpleClock :hours="7.5" :minutes="37.5" />
    <SimpleClock :hours="7.5" :minutes="37.5" />
    <SimpleClock :hours="3" :minutes="30" />
    <SimpleClock :hours="9" :minutes="30" />
    <SimpleClock :hours="0" :minutes="15" />
    <SimpleClock :hours="0" :minutes="45" />
    <SimpleClock :hours="3" :minutes="30" />
    <SimpleClock :hours="9" :minutes="30" />
    <SimpleClock :hours="0" :minutes="15" />
    <SimpleClock :hours="0" :minutes="45" />
    <SimpleClock :hours="7.5" :minutes="37.5" />
    <SimpleClock :hours="7.5" :minutes="37.5" />
  </div>
</template>

<style scoped>
.dot-container {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  width: fit-content;
  height: 100%;
  gap: 4px;
}
</style>
