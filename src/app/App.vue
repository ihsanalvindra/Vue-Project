<template>
  <div class="landing-page">
    <!-- Hero Section -->
    <section class="hero">
      <div class="hero-content">
        <h1>Machine Learning Models</h1>
        <p>Edukasi berbagai model ML & AI secara interaktif</p>
        <button @click="scrollTo('models')">Lihat Model</button>
      </div>
      <svg class="hero-svg" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 600 400">
        <circle cx="300" cy="200" r="150" fill="rgba(255,255,255,0.1)"/>
        <circle cx="400" cy="100" r="80" fill="rgba(255,255,255,0.15)"/>
        <circle cx="200" cy="300" r="60" fill="rgba(255,255,255,0.2)"/>
      </svg>
    </section>

    <!-- Models Section -->
    <section id="models" class="models-section">
      <h2>Macam-macam Model ML</h2>
      <div class="model-cards">
        <div v-for="model in models" :key="model.name" class="card">
          <svg class="card-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
            <path fill="#3b82f6" d="M12 2L15 8H9L12 2Z"/>
          </svg>
          <h3>{{ model.name }}</h3>
          <p>{{ model.description }}</p>
          <p>Use Case: {{ model.usecase }}</p>
        </div>
      </div>
    </section>

    <!-- Chart Section -->
    <section class="chart-section">
      <h2>Perbandingan Model</h2>
      <canvas ref="chartCanvas"></canvas>
    </section>

    <!-- Tips Section -->
    <section class="tips-section">
      <h2>Tips & Tricks</h2>
      <ul>
        <li v-for="tip in tips" :key="tip">
          <svg class="tip-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
            <path fill="#10b981" d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z"/>
          </svg>
          {{ tip }}
        </li>
      </ul>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <p>&copy; 2025 ML Edu | Ihsan Alvindra</p>
      <div class="socials">
        <a href="#">🐦</a>
        <a href="#">💼</a>
        <a href="#">📷</a>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import Chart from 'chart.js/auto'

const scrollTo = (id)=>{
  document.getElementById(id)?.scrollIntoView({behavior:'smooth'})
}

const models = ref([])
const tips = ref([])
const chartCanvas = ref(null)

onMounted(async () => {
  try {
    const modelsRes = await fetch('/data/models.json')
    models.value = await modelsRes.json()

    const tipsRes = await fetch('/data/tips.json')
    tips.value = await tipsRes.json()

    const compRes = await fetch('/data/comparison.json')
    const compData = await compRes.json()

    new Chart(chartCanvas.value, {
      type: 'bar',
      data: {
        labels: ['Accuracy','Speed','Interpretability'],
        datasets: compData.map((item, idx) => ({
          label: item.name,
          data: [item.accuracy, item.speed, item.interpretability],
          backgroundColor: `rgba(${50*(idx+1)},130,246,0.2)`,
          borderColor: `rgba(${50*(idx+1)},130,246,1)`,
          borderWidth: 1
        }))
      },
      options: {
        indexAxis: 'y',
        responsive: true,
        plugins: { tooltip: { mode: 'nearest', intersect: true } },
        scales: { x: { beginAtZero: true }, y: { beginAtZero: true } }
      }
    })
  } catch (err) {
    console.error('Error loading JSON data:', err)
  }
})
</script>

<style>
body { font-family: 'Poppins', sans-serif; margin: 0; }
.landing-page { text-align: center; color: #333; }

/* Hero */
.hero { position: relative; background: linear-gradient(135deg,#4f46e5,#3b82f6); color: #fff; padding: 120px 20px; overflow: hidden;}
.hero h1 { font-size: 3rem; margin-bottom: 1rem; }
.hero p { font-size: 1.2rem; margin-bottom: 2rem; }
.hero button { padding: 12px 30px; background-color: #fff; color: #3b82f6; border: none; border-radius: 30px; font-weight: bold; cursor: pointer; transition: transform 0.3s; }
.hero button:hover { transform: scale(1.05); }
.hero-svg { position: absolute; top:0; left:0; width:100%; height:100%; z-index:0; }

/* Models */
.models-section { padding: 80px 20px; background: #f9fafb; }
.models-section h2 { font-size: 2rem; margin-bottom: 40px; }
.model-cards { display: flex; justify-content: center; flex-wrap: wrap; gap: 24px; }
.card { position: relative; background: #fff; padding: 20px; width: 220px; border-radius: 20px; box-shadow: 0 4px 10px rgba(0,0,0,0.1); transition: transform 0.3s, box-shadow 0.3s; z-index:1; }
.card:hover { transform: translateY(-10px); box-shadow: 0 8px 20px rgba(0,0,0,0.2); }
.card-icon { width: 40px; height: 40px; margin-bottom: 10px; }

/* Chart Section */
.chart-section { padding: 80px 20px; }

/* Tips Section */
.tips-section { padding: 80px 20px; background: #f9fafb; }
.tips-section h2 { margin-bottom: 20px; }
.tips-section ul { list-style: none; padding: 0; max-width: 500px; margin: auto; }
.tips-section li { text-align: left; margin-bottom: 12px; font-size: 1rem; display:flex; align-items:center; gap:8px; }
.tip-icon { width:20px; height:20px; }

/* Footer */
.footer { padding: 40px 20px; background: #1e3a8a; color: #fff; }
.footer .socials { margin-top: 10px; display:flex; justify-content:center; gap:12px; }
.footer .socials a { color:#fff; font-size:1.5rem; text-decoration:none; }
</style>
