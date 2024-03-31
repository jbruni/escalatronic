<script setup>
import { computed, reactive } from 'vue'
import ScaleCircle from './ScaleCircle.vue'

const baseTones = ['C', 'D', 'E', 'F', 'G', 'A', 'B']
const tones = ['C', 'Db', 'D', 'Eb', 'E', 'F', 'F#', 'G', 'Ab', 'A', 'Bb', 'B']
const replacements = {
  C: { 'Db': 'C#', 'D': 'CX', 'B': 'Cb', 'Bb': 'Cbb', 'A#': 'Cbb' },
  D: { 'Eb': 'D#', 'E': 'DX', 'C#': 'Db', 'C': 'Dbb' },
  E: { 'F': 'E#', 'F#': 'EX', 'D#': 'Eb', 'D': 'Ebb', 'Gb': 'EX'  },
  F: { 'Gb': 'F#', 'G': 'FX', 'E': 'Fb', 'Eb': 'Fbb', 'D#': 'Fbb' },
  G: { 'Ab': 'G#', 'A': 'GX', 'F#': 'Gb', 'F': 'Gbb' },
  A: { 'Bb': 'A#', 'B': 'AX', 'G#': 'Ab', 'G': 'Abb' },
  B: { 'C': 'B#', 'C#': 'BX', 'A#': 'Bb', 'A': 'Bbb', 'Db': 'BX' }
}
const increase = {
  St: 1,
  T: 2,
  'T+St': 3
}
const colors = reactive({})

const props = defineProps({
  tone: {
    type: String,
    required: true
  },
  mode: {
    type: String,
    required: true
  },
  useColor: {
    type: String,
    required: true
  }
})

const sequence = computed(() => {
  const result = []
  const prog = props.mode.split(' ')
  let pos = tones.indexOf(props.tone)
  result.push(props.tone)
  for (let i = 0; i < 6; i++) {
    pos += increase[prog[i]]
    if (pos >= tones.length) {
      pos -= tones.length
    }
    result.push(tones[pos])
  }
  return replaceRepeated(result)
})

const sequence2 = computed(() => {
  const result = []
  const seq = []
  seq.push(...Array.from(sequence.value))
  seq.push(...Array.from(sequence.value))
  for (let i = 0; i < 7; i++) {
    result.push(seq[i * 2])
  }
  return result
})

const sequence3 = computed(() => {
  const result = []
  const seq = []
  seq.push(...Array.from(sequence2.value))
  seq.push(...Array.from(sequence2.value))
  for (let i = 0; i < 7; i++) {
    result.push(seq[i * 2])
  }
  return result
})

function replaceRepeated(seq) {
  const result = Array.from(seq)
  const indexFirst = baseTones.indexOf(result[0][0])
  const seqTones = [...baseTones.slice(indexFirst), ...baseTones.slice(0, indexFirst)]
  for (let i = 1; i < result.length; i++) {
    if (result[i][0] === seqTones[i]) {
      continue;
    }
    result[i] = replacements[seqTones[i]][result[i]]
  }
  return result
}

function assignColor(tone) {
  colors[tone] = props.useColor
}
</script>

<template>
  <div class="Scale">
    <ScaleCircle :sequence="sequence" :colors="colors" @clickTone="assignColor" />
    <ScaleCircle :sequence="sequence2" :colors="colors" @clickTone="assignColor" />
    <ScaleCircle :sequence="sequence3" :colors="colors" @clickTone="assignColor" />
  </div>
</template>

<style>
.Scale {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
}
</style>
