<template>
  <div class="tabs py-10" id="categories">
    <div class="flex justify-center gap-4 mb-6">
      <button v-for="cat in categories" :key="cat" @click="active = cat" :class="active===cat ? 'bg-blue-500 text-white' : 'bg-gray-200'" class="px-4 py-2 rounded">
        {{ cat }}
      </button>
    </div>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      <ModelCard v-for="model in filteredModels" :key="model.name" :model="model"/>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import ModelCard from './ModelCard.vue'

const categories = ['Supervised','Unsupervised','Reinforcement','Deep Learning']
const active = ref('Supervised')
const models = ref([])

onMounted(async ()=>{
  const res = await fetch('/data/models.json')
  models.value = await res.json()
})

const filteredModels = computed(()=> models.value.filter(m=>m.category===active.value))
</script>
