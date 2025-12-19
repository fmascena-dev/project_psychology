<template>
  <section id="sobre" class="about">
    <div class="about__container">
      <div class="about__grid">
        <div class="about__image-wrapper">
          <div class="about__image-container">
            <img
              src="https://images.unsplash.com/photo-1551836022-d5d88e9218df?w=600&h=800&fit=crop"
              alt="Bárbara Vilard em seu consultório"
              class="about__image"
            />
          </div>

          <div class="about__image-bg"></div>

          <div class="about__floating-card animate-float">
            <div class="about__status-indicator"></div>
            <span>Aceitando novos pacientes</span>
          </div>
        </div>

        <div class="about__content">
          <span class="about__badge">Sobre Mim</span>

          <h2 class="about__title">
            Uma jornada dedicada ao
            <span class="about__title-highlight">cuidado emocional</span>
          </h2>

          <div class="about__text">
            <p>
              Sou Bárbara Vilard, psicóloga clínica apaixonada por ajudar pessoas
              a encontrarem equilíbrio emocional e qualidade de vida. Minha abordagem
              é baseada na Terapia Cognitivo-Comportamental, aliada a técnicas de
              mindfulness e acolhimento humanizado.
            </p>
            <p>
              Acredito que cada pessoa carrega uma história única e merece ser
              ouvida com respeito e empatia. Meu objetivo é criar um ambiente seguro
              onde você possa explorar seus sentimentos, superar desafios e
              desenvolver ferramentas para uma vida mais plena.
            </p>
          </div>

          <div class="about__credentials">
            <div
              v-for="(item, index) in credentials"
              :key="item.title"
              class="about__credential-item fade-in"
              :style="{ animationDelay: `${index * 0.1 + 0.3}s` }"
            >
              <div class="about__credential-icon">
                <component :is="item.icon" :size="20" />
              </div>
              <div class="about__credential-content">
                <h4 class="about__credential-title">{{ item.title }}</h4>
                <p class="about__credential-description">{{ item.description }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { GraduationCap, Award, Clock, MapPin } from 'lucide-vue-next'

const credentials = [
  {
    icon: GraduationCap,
    title: 'Formação',
    description: 'Graduação em Psicologia pela Universidade Federal'
  },
  {
    icon: Award,
    title: 'Especialização',
    description: 'Pós-graduação em Terapia Cognitivo-Comportamental'
  },
  {
    icon: Clock,
    title: 'Experiência',
    description: 'Mais de 8 anos de atuação clínica'
  },
  {
    icon: MapPin,
    title: 'Atendimento',
    description: 'Online e presencial em São Paulo'
  }
]
</script>

<style scoped lang="scss">
  @use '../styles/about.style.scss';

</style>
