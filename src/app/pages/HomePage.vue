<template>
  <div>
    <Hero @scroll-to="scrollTo"/>
    <CategoryTabs ref="categories"/>
    <ModelComparison/>
    <TipsSection/>
    <Footer/>
    <div class="text-center text-3xl mt-20">Landing Page ML Works</div>
  </div>
</template>


<script setup>
import Hero from '../components/Hero.vue'
import CategoryTabs from '../components/CategoryTabs.vue'
import ModelComparison from '../components/ModelComparison.vue'
import TipsSection from '../components/TipsSection.vue'
import Footer from '../components/Footer.vue'

const scrollTo = (id)=>{
  document.getElementById(id)?.scrollIntoView({behavior:'smooth'})
}
</script>
