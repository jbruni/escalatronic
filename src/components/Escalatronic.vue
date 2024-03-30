<script setup>
import { ref, reactive, computed } from 'vue'
import Scale from './Scale.vue'

const tones = ['C', 'Db', 'D', 'Eb', 'E', 'F', 'F#', 'G', 'Ab', 'A', 'Bb', 'B']
const modes = {
  'Maior (Ionio)': 'T T St T T T St',
  Doriano: 'T St T T T St T',
  Frigiano: 'St T T T St T T',
  'Frigiano dominante': 'St T+St St T St T T',
  Lidio: 'T T T St T T St',
  Mixolidio: 'T T St T T St T',
  'Menor (Aeolio)': 'T St T T St T T',
  'Menor harmônico': 'T St T T St T+St St',
  Locriano: 'St T T St T T T'
}

const modeNames = Object.keys(modes)

const selectedTone = ref(tones[0])
const selectedMode = ref(modeNames[0])
</script>

<template>
  <div>
    <h2>
      Tom:
      <select v-model="selectedTone">
        <option v-for="option in tones" :value="option">
          {{ option }}
        </option>
      </select>
    </h2>
    <h2>
      Modo:
      <select v-model="selectedMode">
        <option v-for="(value, option) in modes" :value="option">
          {{ option }}
        </option>
      </select>
    </h2>
    <Scale :tone="selectedTone" :mode="modes[selectedMode]" />
  </div>
</template>

<style scoped></style>
