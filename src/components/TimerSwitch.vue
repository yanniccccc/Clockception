<script lang="ts" setup>
import { ref } from 'vue'

const isPressed = ref<boolean>(false)

const emit = defineEmits<{
  (e: 'update:isPressed', value: boolean): void
}>()
</script>

<template>
  <div class="switch-container">
    <span
      class="clock-text"
      @click="
        () => {
          isPressed = false
          emit('update:isPressed', isPressed)
        }
      "
      :style="{ color: `${isPressed ? 'var(--secondary)' : 'var(--primary)'}` }"
      >Clock</span
    >
    <button
      class="custom-switch"
      @click="
        () => {
          isPressed = !isPressed
          emit('update:isPressed', isPressed)
        }
      "
    >
      <span :class="{ 'custom-knob': true, 'knob-pressed': isPressed }"></span>
    </button>
    <span
      class="timer-texts"
      @click="
        () => {
          isPressed = true
          emit('update:isPressed', isPressed)
        }
      "
      :style="{ color: `${isPressed ? 'var(--primary)' : 'var(--secondary)'}` }"
      >Timer</span
    >
  </div>
</template>

<style scoped>
.clock-text,
.timer-texts {
  font-size: 1rem;
  color: var(--secondary);
  user-select: none;
  cursor: pointer;
}
.switch-container {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
  flex-direction: row;
}

.custom-switch {
  position: relative;
  all: unset;
  width: 60px;
  height: 30px;
  border-radius: 15px;
  background-color: var(--secondary);
  cursor: pointer;
}

.custom-knob {
  display: block;
  position: relative;
  width: 26px;
  height: 26px;
  background-color: var(--background);
  border-radius: 50%;
  left: 2px;
  transition: transform 0.3s ease;
}

.knob-pressed {
  transform: translateX(30px);
}
</style>
