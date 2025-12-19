<script setup lang="ts">
import Header from './components/Header.vue'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import Services from './components/Services.vue'
import ContactSection from './components/ContactSection.vue'
import Footer from './components/Footer.vue'
import WhatsAppButton from './components/WhatsAppButton.vue'
</script>

<template>
  <div class="min-h-screen">
    <Header />
    <main>
      <HeroSection />
      <Services />
      <AboutSection />
      <ContactSection />
    </main>
    <Footer />
    <WhatsAppButton />
  </div>
</template>

<style>
.min-h-screen {
  min-height: 100vh;
  background: var(--gradient-hero);
}
</style>
