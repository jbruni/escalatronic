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
const selectedColor = ref('#33AA33')

/*
const alpha = (2 * 3.1415) / 7
const r = 100
const q = 100

let css = ""
let x = 0
let y = 0

for (let k = 0; k < 7; k++) {
  x = Math.round((Math.cos((alpha * k * -1) + (3.1415 / 2)) * r) + q) - 20
  y = Math.round((Math.sin((alpha * k * -1) + (3.1415 / 2)) * r) + q) * -1 + 180
  css += `.Seq${k} {\n  top: ${y}px;\n  left: ${x}px;\n}\n\n`
}
*/
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
    <h2>
      Cor:
      <input v-model="selectedColor">
    </h2>
    <br><br><br>
    <Scale :tone="selectedTone" :mode="modes[selectedMode]" :useColor="selectedColor" />
  </div>
</template>

<style scoped></style>
