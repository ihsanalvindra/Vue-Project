<template>
  <div class="card p-6 border rounded-lg shadow hover:shadow-lg transition">
    <div class="text-4xl mb-3">{{ model.icon }}</div>
    <h3 class="font-bold text-xl mb-2">{{ model.name }}</h3>
    <p class="text-gray-700 mb-1">{{ model.description }}</p>
    <p class="text-gray-500 italic">Use case: {{ model.useCase }}</p>
  </div>
</template>

<script setup>
defineProps({
  model: Object
})
</script>
