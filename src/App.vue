<script setup lang="ts">
import Header from './components/Header.vue'
import HeroSection from './components/HeroSection.vue'
import Services from './components/Services.vue'
</script>

<template>
  <Header />
  <div id="home">
    <HeroSection />
  </div>

  <div id="services">
    <Services />
  </div>
</template>

<style scoped></style>
