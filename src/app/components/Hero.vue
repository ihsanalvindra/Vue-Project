<template>
  <section class="hero text-center py-20 bg-gradient-to-r from-blue-500 to-indigo-600 text-white">
    <h1 class="text-5xl font-bold mb-4">Pelajari Berbagai Model Machine Learning</h1>
    <p class="text-xl mb-6">SVM, KNN, Random Forest, Gradient Boosting, CNN, dan banyak lagi — semua dijelaskan secara singkat dan interaktif.</p>
    <button @click="$emit('scroll-to', 'categories')" class="px-6 py-3 bg-white text-blue-600 font-semibold rounded-lg shadow hover:bg-gray-100 transition">Mulai Belajar</button>
  </section>
</template>
