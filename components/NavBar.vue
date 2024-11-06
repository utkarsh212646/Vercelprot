<template>
  <nav class="fixed top-0 w-full bg-white/80 backdrop-blur-sm z-50 shadow-sm">
    <div class="container mx-auto px-4">
      <div class="flex justify-between items-center h-16">
        <a href="#" class="text-2xl font-bold text-primary">Portfolio</a>
        
        <!-- Mobile menu button -->
        <button @click="isOpen = !isOpen" class="lg:hidden">
          <span class="sr-only">Open menu</span>
          <Bars3Icon v-if="!isOpen" class="h-6 w-6" />
          <XMarkIcon v-else class="h-6 w-6" />
        </button>

        <!-- Desktop menu -->
        <div class="hidden lg:flex space-x-8">
          <a v-for="item in menuItems" 
             :key="item.href" 
             :href="item.href"
             class="text-gray-700 hover:text-primary transition-colors">
            {{ item.label }}
          </a>
        </div>
      </div>
    </div>

    <!-- Mobile menu -->
    <Transition
      enter-active-class="transition duration-200 ease-out"
      enter-from-class="transform -translate-y-full"
      enter-to-class="transform translate-y-0"
      leave-active-class="transition duration-200 ease-in"
      leave-from-class="transform translate-y-0"
      leave-to-class="transform -translate-y-full"
    >
      <div v-if="isOpen" class="lg:hidden bg-white border-t">
        <div class="container mx-auto px-4 py-2">
          <a v-for="item in menuItems" 
             :key="item.href" 
             :href="item.href"
             @click="isOpen = false"
             class="block py-2 text-gray-700 hover:text-primary transition-colors">
            {{ item.label }}
          </a>
        </div>
      </div>
    </Transition>
  </nav>
</template>

<script setup>
import { ref } from 'vue'
import { Bars3Icon, XMarkIcon } from '@heroicons/vue/24/outline'

const isOpen = ref(false)

const menuItems = [
  { label: 'Home', href: '#home' },
  { label: 'About', href: '#about' },
  { label: 'Projects', href: '#projects' },
  { label: 'Skills', href: '#skills' },
  { label: 'Contact', href: '#contact' }
]
</script>