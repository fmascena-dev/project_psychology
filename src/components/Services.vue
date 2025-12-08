<template>
  <section class="section services" id="services">
    <div class="container">
      <h2 class="section-title">Meus Serviços</h2>

      <div class="carousel-container" ref="containerRef">
        <div
          class="carousel-track"
          :style="{ transform: `translateX(-${trackTranslate}px)` }"
          ref="trackRef"
        >
          <div
            v-for="(service, index) in services"
            :key="index"
            class="service-card"
            ref="cardRefs"
          >
            <div class="service-icon">{{ service.icon }}</div>
            <h3>{{ service.title }}</h3>
            <p>{{ service.text }}</p>
          </div>
        </div>
      </div>

      <div class="carousel-controls">
        <button class="carousel-btn" @click="prevSlide">
          <i class="pi pi-arrow-left"></i>
        </button>
        <button class="carousel-btn" @click="nextSlide">
          <i class="pi pi-arrow-right"></i>
        </button>
      </div>

      <div class="carousel-dots">
        <span
          v-for="(p, i) in pages"
          :key="i"
          class="dot"
          :class="{ active: i === pageIndex }"
          @click="goToPage(i)"
        ></span>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount, nextTick, computed } from 'vue'

const services = [
  { icon: '🧠', title: 'Terapia Individual', text: 'Atendimento personalizado...' },
  { icon: '👥', title: 'Terapia de Casal', text: 'Apoio para melhorar comunicação...' },
  { icon: '😌', title: 'Gestão de Ansiedade', text: 'Técnicas para lidar com ansiedade...' },
  { icon: '💪', title: 'Autoestima', text: 'Fortalecimento da autoconfiança...' },
]

const visibleCards = ref(2)
const gapPx = 24

const currentIndex = ref(0)
const containerRef = ref<HTMLElement | null>(null)
const trackRef = ref<HTMLElement | null>(null)
const cardRefs = ref<Array<HTMLElement>>([])

const cardWidth = ref(0)
const trackTranslate = ref(0)

const pages = computed(() => Math.max(1, Math.ceil(services.length - visibleCards.value + 1)))
const pageIndex = computed(() => {
  return currentIndex.value
})

const recalc = async () => {
  await nextTick()
  const firstCard = (cardRefs.value && cardRefs.value[0]) || null
  if (!firstCard || !containerRef.value) return

  cardWidth.value = firstCard.getBoundingClientRect().width
  trackTranslate.value = currentIndex.value * (cardWidth.value + gapPx)
}

const nextSlide = () => {
  const maxIndex = Math.max(0, services.length - visibleCards.value)
  currentIndex.value = currentIndex.value >= maxIndex ? 0 : currentIndex.value + 1
  trackTranslate.value = currentIndex.value * (cardWidth.value + gapPx)
}

const prevSlide = () => {
  const maxIndex = Math.max(0, services.length - visibleCards.value)
  currentIndex.value = currentIndex.value <= 0 ? maxIndex : currentIndex.value - 1
  trackTranslate.value = currentIndex.value * (cardWidth.value + gapPx)
}

const goToPage = (page: number) => {
  const maxIndex = Math.max(0, services.length - visibleCards.value)
  const idx = Math.min(maxIndex, Math.max(0, page))
  currentIndex.value = idx
  trackTranslate.value = currentIndex.value * (cardWidth.value + gapPx)
}

let resizeObserver: ResizeObserver | null = null
onMounted(async () => {
  const cards = trackRef.value?.querySelectorAll('.service-card') || []
  cardRefs.value = Array.from(cards) as HTMLElement[]

  await recalc()

  if (containerRef.value) {
    resizeObserver = new ResizeObserver(() => recalc())
    resizeObserver.observe(containerRef.value)
  }

  const handleWindowResize = () => {
    const w = window.innerWidth
    if (w < 720) visibleCards.value = 1
    else visibleCards.value = 2
    const maxIndex = Math.max(0, services.length - visibleCards.value)
    if (currentIndex.value > maxIndex) currentIndex.value = maxIndex
    recalc()
  }
  window.addEventListener('resize', handleWindowResize)
  handleWindowResize()
})

onBeforeUnmount(() => {
  if (resizeObserver && containerRef.value) resizeObserver.unobserve(containerRef.value)
  window.removeEventListener('resize', () => {})
})
</script>

<style scoped lang="scss">
@use '../styles/services.style.scss';
</style>
