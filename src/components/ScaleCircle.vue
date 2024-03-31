<script setup>
import ScaleCircle from './ScaleCircle.vue'

const props = defineProps({
  sequence: {
    type: Array,
    required: true
  },
  colors: {
    type: Object,
    required: true
  }
})

const emit = defineEmits(['clickTone'])
</script>

<template>
  <div class="ScaleCircle">
    <span
      v-for="tone, index in sequence"
      :class="`Seq${index}`"
      :style="{ 'background-color': colors[tone] ? colors[tone] : 'transparent' }"
      @click="emit('clickTone', tone)"
    >{{ tone }}</span>
  </div>
</template>

<style>
.ScaleCircle {
  width: 200px;
  height: 200px;
  border: 1px solid #DDFFDD;
  border-radius: 100px;
  margin-bottom: 50px;
  margin-top: 40px;
  margin-left: 40px;
  margin-right: 40px;
  position: relative;
  user-select: none;
}

.ScaleCircle span {
  display: block;
  width: 40px;
  height: 40px;
  line-height: 40px;
  text-align: center;
  font-size: 20px;
  border-radius: 30px;
  border: 1px solid green;
  position: absolute;
  cursor: pointer;
}

.Seq0 {
  top: -20px;
  left: 80px;
}

.Seq1 {
  top: 18px;
  left: 158px;
}

.Seq2 {
  top: 102px;
  left: 177px;
}

.Seq3 {
  top: 170px;
  left: 123px;
}

.Seq4 {
  top: 170px;
  left: 37px;
}

.Seq5 {
  top: 102px;
  left: -17px;
}

.Seq6 {
  top: 18px;
  left: 2px;
}


</style>
