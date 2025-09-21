<template>
  <section class="py-10">
    <h2 class="text-3xl font-bold text-center mb-6">Perbandingan Model</h2>
    <canvas ref="chartCanvas"></canvas>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import Chart from 'chart.js/auto'

const chartCanvas = ref(null)

onMounted(async ()=>{
  const res = await fetch('/data/comparison.json')
  const data = await res.json()

  new Chart(chartCanvas.value,{
    type:'radar',
    data:{
      labels:['Accuracy','Speed','Interpretability'],
      datasets:data.map(d=>({
        label:d.name,
        data:[d.accuracy,d.speed,d.interpretability],
        fill:true,
        backgroundColor:'rgba(59,130,246,0.2)',
        borderColor:'#3b82f6'
      }))
    },
    options:{responsive:true, scales:{r:{beginAtZero:true}}}
  })
})
</script>
