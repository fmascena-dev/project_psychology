<template>
  <section id="servicos" class="services">
    <div class="container">
      <div class="header">
        <span class="badge">Serviços</span>
        <h2>Como posso te ajudar</h2>
        <p>
          Ofereço diferentes abordagens terapêuticas para atender às suas
          necessidades específicas
        </p>
      </div>

      <div class="carousel-wrapper">
        <button
          class="nav-btn left"
          :class="{ hidden: !canScrollLeft }"
          :disabled="!canScrollLeft"
          @click="scroll('left')"
        >
          <ChevronLeft />
        </button>

        <button
          class="nav-btn right"
          :class="{ hidden: !canScrollRight }"
          :disabled="!canScrollRight"
          @click="scroll('right')"
        >
          <ChevronRight />
        </button>

        <div
          ref="carouselRef"
          class="carousel"
          @scroll="checkScroll"
        >
          <div
            v-for="(service, index) in services"
            :key="service.title"
            class="card-wrapper"
            :style="{ animationDelay: `${index * 0.1}s` }"
          >
            <div class="card">
              <div class="icon" :class="service.color">
                <component :is="service.icon" />
              </div>

              <h3>{{ service.title }}</h3>
              <p>{{ service.description }}</p>
            </div>
          </div>
        </div>
      </div>

      <div class="dots">
        <span v-for="(_, i) in services" :key="i" />
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";
import {
  ChevronLeft,
  ChevronRight,
  Brain,
  Heart,
  Users,
  Sparkles,
  Target,
  MessageCircle,
} from "lucide-vue-next";

type Direction = "left" | "right";

const services = [
  {
    icon: Brain,
    title: "Terapia Individual",
    description:
      "Sessões personalizadas para adultos que buscam autoconhecimento, desenvolvimento pessoal e superação de desafios emocionais.",
    color: "primary",
  },
  {
    icon: Heart,
    title: "Ansiedade e Estresse",
    description:
      "Tratamento especializado para transtornos de ansiedade, síndrome do pânico e gerenciamento do estresse.",
    color: "accent",
  },
  {
    icon: Users,
    title: "Terapia de Casal",
    description:
      "Acompanhamento para casais que desejam melhorar a comunicação e resolver conflitos.",
    color: "green",
  },
  {
    icon: Sparkles,
    title: "Desenvolvimento Pessoal",
    description:
      "Processo terapêutico focado em autoestima e inteligência emocional.",
    color: "accent",
  },
  {
    icon: Target,
    title: "Burnout e Carreira",
    description:
      "Suporte para profissionais enfrentando esgotamento e transições de carreira.",
    color: "primary",
  },
  {
    icon: MessageCircle,
    title: "Atendimento Online",
    description:
      "Sessões por videochamada com a mesma qualidade do atendimento presencial.",
    color: "accent",
  },
];

const carouselRef = ref<HTMLDivElement | null>(null);
const canScrollLeft = ref(false);
const canScrollRight = ref(true);

const checkScroll = () => {
  if (!carouselRef.value) return;

  const { scrollLeft, scrollWidth, clientWidth } = carouselRef.value;

  canScrollLeft.value = scrollLeft > 0;
  canScrollRight.value = scrollLeft < scrollWidth - clientWidth - 10;
};

const scroll = (direction: Direction) => {
  if (!carouselRef.value) return;

  carouselRef.value.scrollBy({
    left: direction === "left" ? -340 : 340,
    behavior: "smooth",
  });
};

onMounted(() => {
  checkScroll();
});
</script>

<style scoped lang="scss">
@use "../styles/services.style.scss";
</style>
