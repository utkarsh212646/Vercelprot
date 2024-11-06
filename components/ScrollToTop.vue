<template>
  <button
    v-show="showButton"
    @click="scrollToTop"
    class="fixed bottom-8 right-8 bg-primary text-white w-12 h-12 rounded-full shadow-lg flex items-center justify-center hover:bg-primary/90 transition-colors z-50"
    v-motion
    :initial="{ opacity: 0, scale: 0.5 }"
    :enter="{ opacity: 1, scale: 1 }"
  >
    <ArrowUpIcon class="w-6 h-6" />
  </button>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { ArrowUpIcon } from '@heroicons/vue/24/outline'

const showButton = ref(false)

const checkScroll = () => {
  showButton.value = window.scrollY > 500
}

const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: 'smooth'
  })
}

onMounted(() => {
  window.addEventListener('scroll', checkScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', checkScroll)
})
</script>