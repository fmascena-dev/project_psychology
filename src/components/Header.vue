<template>
  <header :class="['header', { 'header--scrolled': isScrolled }]">
    <div class="header__container">
      <div class="header__content">
        <a href="#inicio" class="header__logo" @click.prevent="scrollToSection('#inicio')">
          <span class="header__logo-text">Bárbara Vilard</span>
        </a>

        <nav class="header__nav">
          <a
            v-for="item in navItems"
            :key="item.href"
            :href="item.href"
            class="header__nav-link"
            @click.prevent="scrollToSection(item.href)"
          >
            {{ item.label }}
          </a>
        </nav>

        <div class="header__actions">
          <button
            class="header__theme-toggle"
            @click="toggleTheme"
            :aria-label="theme === 'light' ? 'Ativar modo escuro' : 'Ativar modo claro'"
          >
            <svg
              :class="['header__theme-icon', { 'header__theme-icon--hidden': theme !== 'light' }]"
              xmlns="http://www.w3.org/2000/svg"
              width="20"
              height="20"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <circle cx="12" cy="12" r="4" />
              <path d="M12 2v2" />
              <path d="M12 20v2" />
              <path d="m4.93 4.93 1.41 1.41" />
              <path d="m17.66 17.66 1.41 1.41" />
              <path d="M2 12h2" />
              <path d="M20 12h2" />
              <path d="m6.34 17.66-1.41 1.41" />
              <path d="m19.07 4.93-1.41 1.41" />
            </svg>
            <svg
              :class="['header__theme-icon', { 'header__theme-icon--hidden': theme !== 'dark' }]"
              xmlns="http://www.w3.org/2000/svg"
              width="20"
              height="20"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path d="M12 3a6 6 0 0 0 9 9 9 9 0 1 1-9-9Z" />
            </svg>
          </button>

          <button
            class="header__menu-toggle"
            @click="isMenuOpen = !isMenuOpen"
            :aria-label="isMenuOpen ? 'Fechar menu' : 'Abrir menu'"
          >
            <svg
              v-if="!isMenuOpen"
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <line x1="4" x2="20" y1="12" y2="12" />
              <line x1="4" x2="20" y1="6" y2="6" />
              <line x1="4" x2="20" y1="18" y2="18" />
            </svg>
            <svg
              v-else
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path d="M18 6 6 18" />
              <path d="m6 6 12 12" />
            </svg>
          </button>
        </div>
      </div>
    </div>

    <div :class="['header__mobile-nav', { 'header__mobile-nav--open': isMenuOpen }]">
      <nav class="header__mobile-nav-container">
        <a
          v-for="(item, index) in navItems"
          :key="item.href"
          :href="item.href"
          class="header__mobile-nav-link"
          :style="{ animationDelay: `${index * 0.1}s` }"
          @click.prevent="scrollToSection(item.href)"
        >
          {{ item.label }}
        </a>
      </nav>
    </div>
  </header>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const navItems = [
  { label: 'Início', href: '#inicio' },
  { label: 'Serviços', href: '#servicos' },
  { label: 'Sobre Mim', href: '#sobre' },
  { label: 'Contato', href: '#contato' },
]

const theme = ref<'light' | 'dark'>('light')
const isMenuOpen = ref(false)
const isScrolled = ref(false)

const toggleTheme = () => {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
  document.documentElement.classList.toggle('dark')
}

const handleScroll = () => {
  isScrolled.value = window.scrollY > 20
}

const scrollToSection = (href: string) => {
  const element = document.querySelector(href)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
  isMenuOpen.value = false
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)

  // Check initial theme
  if (document.documentElement.classList.contains('dark')) {
    theme.value = 'dark'
  }
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style lang="scss" scoped>
@use '../styles/header.style.scss' as *;
</style>
