<template>
  <section id="contato" class="contact">
    <div class="contact__container">
      <div class="contact__header">
        <span class="contact__badge">Contato</span>
        <h2 class="contact__title">Vamos conversar?</h2>
        <p class="contact__subtitle">
          Entre em contato para agendar sua consulta ou tirar dúvidas. Estou aqui para te ajudar.
        </p>
      </div>

      <div class="contact__grid">
        <div class="contact__info">
          <div
            v-for="(item, index) in contactInfo"
            :key="item.label"
            class="contact__info-item"
            :style="{ animationDelay: `${index * 0.1}s` }"
          >
            <div class="contact__info-icon">
              <component :is="item.icon" :size="20" />
            </div>
            <div class="contact__info-content">
              <p class="contact__info-label">{{ item.label }}</p>
              <p class="contact__info-value">{{ item.value }}</p>
            </div>
          </div>
        </div>

        <div class="contact__form-wrapper">
          <form @submit.prevent="handleSubmit" class="contact__form">
            <div class="contact__form-row">
              <div class="contact__form-group">
                <label for="name" class="contact__label">Nome completo</label>
                <input
                  id="name"
                  v-model="formData.name"
                  type="text"
                  placeholder="Seu nome"
                  required
                  class="contact__input"
                />
              </div>
              <div class="contact__form-group">
                <label for="email" class="contact__label">E-mail</label>
                <input
                  id="email"
                  v-model="formData.email"
                  type="email"
                  placeholder="seu@email.com"
                  required
                  class="contact__input"
                />
              </div>
            </div>

            <div class="contact__form-group">
              <label for="phone" class="contact__label">Telefone / WhatsApp</label>
              <input
                id="phone"
                v-model="formData.phone"
                type="tel"
                placeholder="(11) 99999-9999"
                class="contact__input"
              />
            </div>

            <div class="contact__form-group">
              <label for="message" class="contact__label">Mensagem</label>
              <textarea
                id="message"
                v-model="formData.message"
                placeholder="Conte um pouco sobre como posso te ajudar..."
                rows="4"
                required
                class="contact__textarea"
              ></textarea>
            </div>

            <button type="submit" :disabled="isSubmitting" class="contact__submit">
              <span v-if="!isSubmitting">
                Enviar mensagem
                <Send :size="20" class="contact__submit-icon" />
              </span>
              <span v-else>Enviando...</span>
            </button>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { Send, Mail, Phone, MapPin, Clock } from 'lucide-vue-next'

const contactInfo = [
  {
    icon: Mail,
    label: 'E-mail',
    value: 'contato@barbaravilard.com.br',
  },
  {
    icon: Phone,
    label: 'Telefone',
    value: '(11) 99999-9999',
  },
  {
    icon: MapPin,
    label: 'Endereço',
    value: 'São Paulo, SP',
  },
  {
    icon: Clock,
    label: 'Horário',
    value: 'Seg - Sex: 8h às 20h',
  },
]

const isSubmitting = ref(false)
const formData = ref({
  name: '',
  email: '',
  phone: '',
  message: '',
})

const handleSubmit = async () => {
  isSubmitting.value = true

  await new Promise((resolve) => setTimeout(resolve, 1000))

  alert('Mensagem enviada! Entrarei em contato em breve. Obrigada!')

  formData.value = {
    name: '',
    email: '',
    phone: '',
    message: '',
  }

  isSubmitting.value = false
}
</script>

<style scoped lang="scss">
@use '../styles/contact.style.scss' as *;
</style>
