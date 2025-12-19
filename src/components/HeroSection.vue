<template>
  <section id="inicio" class="hero">
    <!-- Background decoration -->
    <div class="hero__bg-decoration">
      <div class="hero__bg-blob hero__bg-blob--top"></div>
      <div class="hero__bg-blob hero__bg-blob--bottom"></div>
    </div>

    <div class="hero__container">
      <div class="hero__grid">
        <!-- Text Content -->
        <div class="hero__content">
          <div class="hero__badge fade-in" style="animation-delay: 0.2s">
            <Heart :size="16" />
            Psicóloga Clínica | CRP 05/65774
          </div>

          <h1 class="hero__title fade-in-left" style="animation-delay: 0.3s">
            Cuidando da sua
            <span class="hero__title-highlight">saúde mental</span>
            com acolhimento e profissionalismo
          </h1>

          <p class="hero__description fade-in" style="animation-delay: 0.5s">
            Olá, eu sou Bárbara Vilard. Ofereço um espaço seguro e acolhedor
            para você explorar seus sentimentos e desenvolver ferramentas para
            uma vida mais equilibrada.
          </p>

          <div class="hero__actions fade-in" style="animation-delay: 0.7s">
            <button class="hero__btn hero__btn--primary" @click="scrollToContact">
              Agendar consulta
              <ArrowRight :size="20" class="hero__btn-icon" />
            </button>

            <button class="hero__btn hero__btn--outline" @click="scrollToAbout">
              Conheça meu trabalho
            </button>
          </div>

          <!-- Trust indicators -->
          <div class="hero__trust fade-in" style="animation-delay: 0.9s">
            <div class="hero__trust-item">
              <Brain :size="22" />
              <span>Terapia Cognitivo-Comportamental</span>
            </div>
            <div class="hero__trust-item">
              <Shield :size="22" />
              <span>Atendimento Online e Presencial</span>
            </div>
          </div>
        </div>

        <!-- Image -->
        <div class="hero__image-wrapper fade-in-right" style="animation-delay: 0.4s">
          <div class="hero__image-container">
            <!-- Background shape -->
            <div class="hero__image-bg"></div>

            <!-- Image -->
            <div class="hero__image">
              <img
                src="/photo1.jpeg"
                loading="lazy"
                alt="Bárbara Vilard - Psicóloga"
              />
            </div>

            <!-- Floating decoration -->
            <div class="hero__floating-card animate-float">
              <div class="hero__floating-icon">
                <Heart :size="24" />
              </div>
              <div class="hero__floating-info">
                <p class="hero__floating-number">+500</p>
                <p class="hero__floating-text">Vidas transformadas</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ArrowRight, Heart, Brain, Shield } from 'lucide-vue-next'

const scrollToContact = () => {
  const element = document.querySelector('#contato')
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}

const scrollToAbout = () => {
  const element = document.querySelector('#sobre')
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}
</script>

<style scoped lang="scss">
  @use "../styles/hero-section.style.scss" as *;

</style>
