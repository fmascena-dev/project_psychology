<template>
  <a
    :href="whatsappUrl"
    target="_blank"
    rel="noopener noreferrer"
    class="whatsapp-button"
    aria-label="Contato via WhatsApp"
  >
    <div class="whatsapp-button__wrapper">
      <div class="whatsapp-button__pulse"></div>

      <div class="whatsapp-button__circle">
        <img src="/whatsapp.svg" alt="" width="40px" height="40px" />
      </div>

      <div class="whatsapp-button__tooltip">
        Fale comigo no WhatsApp
        <div class="whatsapp-button__tooltip-arrow"></div>
      </div>
    </div>
  </a>
</template>

<script setup lang="ts">
import { computed } from 'vue'

const phoneNumber = '5521992071012'
const message = 'Olá! Gostaria de agendar uma consulta com a Dra. Bárbara Vilard.'

const whatsappUrl = computed(() => {
  const encodedMessage = encodeURIComponent(message)
  return `https://wa.me/${phoneNumber}?text=${encodedMessage}`
})
</script>

<style scoped lang="scss">
.whatsapp-button {
  position: fixed;
  bottom: 1.5rem;
  right: 1.5rem;
  z-index: 50;
  text-decoration: none;

  &__wrapper {
    position: relative;
  }

  &__pulse {
    position: absolute;
    inset: 0;
    background-color: #10b981;
    border-radius: 50%;
    animation: ping 1.5s cubic-bezier(0, 0, 0.2, 1) infinite;
    opacity: 0.3;
  }

  &__circle {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 3.5rem;
    height: 3.5rem;
    background-color: #25d366;
    border-radius: 50%;
    box-shadow: 0 8px 32px hsl(150 30% 15% / 0.1);
    color: white;
    transition: all 0.3s ease;

    &:hover {
      box-shadow: 0 12px 40px hsl(150 30% 15% / 0.15);
      transform: scale(1.1);
    }
  }

  &__tooltip {
    position: absolute;
    bottom: 100%;
    right: 0;
    margin-bottom: 0.5rem;
    padding: 0.75rem 1rem;
    background-color: hsl(var(--card));
    border-radius: 0.5rem;
    box-shadow: 0 4px 16px hsl(150 30% 15% / 0.08);
    font-size: 0.875rem;
    font-weight: 500;
    color: hsl(var(--foreground));
    white-space: nowrap;
    opacity: 0;
    visibility: hidden;
    transition: all 0.3s ease;
    transform: translateY(0);

    .whatsapp-button:hover & {
      opacity: 1;
      visibility: visible;
      transform: translateY(-0.25rem);
    }
  }

  &__tooltip-arrow {
    position: absolute;
    bottom: 0;
    right: 1rem;
    width: 0.5rem;
    height: 0.5rem;
    background-color: hsl(var(--card));
    transform: translateY(50%) rotate(45deg);
  }
}

@keyframes ping {
  75%,
  100% {
    transform: scale(2);
    opacity: 0;
  }
}
</style>
