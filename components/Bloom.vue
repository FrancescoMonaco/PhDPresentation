<script setup>
import { ref, onMounted } from 'vue'
import { gsap } from 'gsap'

const dims = Array.from({ length: 20 }, (_, i) => ({
  id: i,
  selected: false,
  estimated: false
}))

const selectedDims = ref([])
const estimatedDims = ref([])

function runAnimation() {
  const selected = [2, 5, 8, 13, 16]
  const estimated = dims.map(d => d.id).filter(id => !selected.includes(id))

  selectedDims.value = selected
  estimatedDims.value = estimated

  dims.forEach(d => {
    d.selected = false
    d.estimated = false
  })

  gsap.timeline({ repeat: -1, repeatDelay: 1 })
    .set('.dim', { opacity: 0.2, backgroundColor: '#ccc' })
    .to('.vectorA, .vectorB', { opacity: 1, duration: 0.5 }, 0)
    .to('.bloom-filter', { opacity: 1, scale: 1, duration: 0.5 }, 0.5)
    .to(selected.map(i => `.dim-A-${i}, .dim-B-${i}`), {
      backgroundColor: '#34d399', // green
      opacity: 1,
      duration: 0.5,
      onStart() {
        selected.forEach(i => {
          dims[i].selected = true
        })
      }
    }, 1.0)
    .to(estimated.map(i => `.dim-A-${i}, .dim-B-${i}`), {
      backgroundColor: '#fbbf24', // yellow
      opacity: 0.6,
      duration: 0.5,
      onStart() {
        estimated.forEach(i => {
          dims[i].estimated = true
        })
      }
    }, 2.0)
}

onMounted(runAnimation)
</script>

<template>
  <div class="flex flex-col items-center space-y-4">
    <div class="text-lg font-bold">Bloom Filter Approximation</div>
    <div class="flex flex-col items-start">
      <div class="text-sm mb-1">Element A</div>
      <div class="vectorA flex space-x-1">
        <div
          v-for="d in dims"
          :key="'a' + d.id"
          class="w-4 h-4 dim"
          :class="'dim-A-' + d.id"
          :style="{ backgroundColor: d.selected ? '#34d399' : d.estimated ? '#fbbf24' : '#ccc' }"
        />
      </div>
      <div class="text-sm mt-2 mb-1">Element B</div>
      <div class="vectorB flex space-x-1">
        <div
          v-for="d in dims"
          :key="'b' + d.id"
          class="w-4 h-4 dim"
          :class="'dim-B-' + d.id"
          :style="{ backgroundColor: d.selected ? '#34d399' : d.estimated ? '#fbbf24' : '#ccc' }"
        />
      </div>
    </div>
    <div class="bloom-filter text-center mt-4 text-sm bg-indigo-600 text-white px-4 py-2 rounded shadow opacity-0 scale-50">
      Bloom Filter selects the best dimensions and estimates the others
    </div>
    <div class="mt-2 text-xs text-gray-500">Green = Selected, Yellow = Estimated</div>
  </div>
</template>

<style scoped>
.dim {
  transition: background-color 0.3s ease;
  border-radius: 2px;
}
</style>
