<template>
  <section class="py-10 bg-gray-100">
    <h2 class="text-3xl font-bold text-center mb-6">Tips Belajar Machine Learning</h2>
    <ul class="max-w-3xl mx-auto space-y-4 list-disc list-inside">
      <li v-for="tip in tips" :key="tip.tip">{{ tip.tip }}</li>
    </ul>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const tips = ref([])

onMounted(async ()=>{
  const res = await fetch('/data/tips.json')
  tips.value = await res.json()
})
</script>
