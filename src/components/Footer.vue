<template>
  <footer class="footer">
    <div class="footer__container">
      <div class="footer__content">
        <div class="footer__logo">
          <span class="footer__logo-text">Bárbara Vilard</span>
        </div>

        <div class="footer__social">
          <a
            v-for="social in socialLinks"
            :key="social.label"
            :href="social.href"
            target="_blank"
            rel="noopener noreferrer"
            class="footer__social-link"
            :aria-label="social.label"
          >
            <component :is="social.icon" :size="20" />
          </a>
        </div>
      </div>

      <div class="footer__bottom">
        <p class="footer__copyright">
          © {{ currentYear }} Bárbara Vilard. Feito com
          <Heart :size="16" class="footer__heart" />
          por
          <span class="footer__author"><a href="https://https://www.instagram.com/f_mascena.dev/">Felipe Mascena</a></span>
        </p>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
import { computed, h } from 'vue'
import { Heart, Mail } from 'lucide-vue-next'

const InstagramIcon = () => h('svg', {
  xmlns: 'http://www.w3.org/2000/svg',
  width: '20',
  height: '20',
  viewBox: '0 0 24 24',
  fill: 'none',
  stroke: 'currentColor',
  'stroke-width': '2',
  'stroke-linecap': 'round',
  'stroke-linejoin': 'round'
}, [
  h('rect', { x: '2', y: '2', width: '20', height: '20', rx: '5', ry: '5' }),
  h('path', { d: 'M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z' }),
  h('line', { x1: '17.5', y1: '6.5', x2: '17.51', y2: '6.5' })
])

const LinkedinIcon = () => h('svg', {
  xmlns: 'http://www.w3.org/2000/svg',
  width: '20',
  height: '20',
  viewBox: '0 0 24 24',
  fill: 'none',
  stroke: 'currentColor',
  'stroke-width': '2',
  'stroke-linecap': 'round',
  'stroke-linejoin': 'round'
}, [
  h('path', { d: 'M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z' }),
  h('rect', { x: '2', y: '9', width: '4', height: '12' }),
  h('circle', { cx: '4', cy: '4', r: '2' })
])

const socialLinks = [
  { icon: InstagramIcon, href: 'https://www.instagram.com/psi.barbaravilard/', label: 'Instagram', isComponent: true },
  { icon: LinkedinIcon, href: '#', label: 'LinkedIn', isComponent: true },
  { icon: Mail, href: 'mailto:contato@barbaravilard.com.br', label: 'Email', isComponent: true },
]

const currentYear = computed(() => new Date().getFullYear())
</script>

<style scoped lang="scss">
@use '../styles/footer.style.scss' as *;
</style>
