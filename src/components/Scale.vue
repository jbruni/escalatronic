<script setup>
import { computed } from 'vue'

const tones = ['C', 'Db', 'D', 'Eb', 'E', 'F', 'F#', 'G', 'Ab', 'A', 'Bb', 'B']
const increase = {
  'St': 1,
  'T': 2,
  'T+St': 3
}

const props = defineProps({
  tone: {
    type: String,
    required: true
  },
  mode: {
    type: String,
    required: true
  }
})

const sequence = computed(() => {
  const result = [];
  const prog = props.mode.split(' ')
  let pos = tones.indexOf(props.tone);
  result.push(props.tone)
  for (let i = 0; i < 6; i++) {
    pos += increase[prog[i]]
    if (pos >= tones.length) {
      pos -= tones.length
    }
    result.push(tones[pos])
  }
  return result;
})

const sequence2 = computed(() => {
  const result = []
  const seq = []
  seq.push(...sequence.value)
  seq.push(...sequence.value)
  for (let i = 0; i < 7; i++) {
    result.push(seq[i*2])
  }
  return result
})

const sequence3 = computed(() => {
  const result = []
  const seq = []
  seq.push(...sequence2.value)
  seq.push(...sequence2.value)
  for (let i = 0; i < 7; i++) {
    result.push(seq[i*2])
  }
  return result
})
</script>

<template>
  <div>
    {{ sequence.join(' ') }}
    <br>
    {{ sequence2.join(' ') }}
    <br>
    {{ sequence3.join(' ') }}
  </div>
</template>

<style scoped></style>
