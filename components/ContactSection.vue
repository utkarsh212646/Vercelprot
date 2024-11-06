<template>
  <section id="contact" class="section bg-gray-50">
    <div class="container">
      <h2 class="text-4xl font-bold text-center mb-16">Get in Touch</h2>
      
      <div class="grid md:grid-cols-2 gap-12">
        <div
          v-motion
          :initial="{ opacity: 0, x: -50 }"
          :enter="{ opacity: 1, x: 0 }"
        >
          <h3 class="text-2xl font-semibold mb-6">Contact Information</h3>
          <div class="space-y-4">
            <div v-for="(item, index) in contactInfo" :key="index" class="flex items-center gap-4">
              <div class="w-12 h-12 rounded-full bg-primary/10 flex items-center justify-center shrink-0">
                <component :is="item.icon" class="w-6 h-6 text-primary" />
              </div>
              <div>
                <h4 class="font-medium">{{ item.label }}</h4>
                <p class="text-gray-600">{{ item.value }}</p>
              </div>
            </div>
          </div>
          
          <div class="mt-8">
            <h4 class="font-medium mb-4">Follow Me</h4>
            <div class="flex gap-4">
              <a 
                v-for="social in socialLinks" 
                :key="social.name"
                :href="social.url"
                target="_blank"
                class="w-10 h-10 rounded-full bg-gray-200 hover:bg-primary hover:text-white flex items-center justify-center transition-colors"
              >
                <component :is="social.icon" class="w-5 h-5" />
              </a>
            </div>
          </div>
        </div>
        
        <form 
          @submit.prevent="handleSubmit"
          class="space-y-6"
          v-motion
          :initial="{ opacity: 0, x: 50 }"
          :enter="{ opacity: 1, x: 0 }"
        >
          <div>
            <label for="name" class="block text-sm font-medium text-gray-700">Name</label>
            <input
              type="text"
              id="name"
              v-model="form.name"
              class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-primary focus:ring-primary"
              required
            />
          </div>
          
          <div>
            <label for="email" class="block text-sm font-medium text-gray-700">Email</label>
            <input
              type="email"
              id="email"
              v-model="form.email"
              class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-primary focus:ring-primary"
              required
            />
          </div>
          
          <div>
            <label for="message" class="block text-sm font-medium text-gray-700">Message</label>
            <textarea
              id="message"
              v-model="form.message"
              rows="4"
              class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-primary focus:ring-primary"
              required
            ></textarea>
          </div>
          
          <button 
            type="submit"
            class="btn btn-primary w-full"
            :disabled="isSubmitting"
          >
            <span v-if="isSubmitting">Sending...</span>
            <span v-else>Send Message</span>
          </button>
        </form>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
import {
  EnvelopeIcon,
  PhoneIcon,
  MapPinIcon
} from '@heroicons/vue/24/outline'

const form = ref({
  name: '',
  email: '',
  message: ''
})

const isSubmitting = ref(false)

const contactInfo = [
  {
    icon: EnvelopeIcon,
    label: 'Email',
    value: 'your.email@example.com'
  },
  {
    icon: PhoneIcon,
    label: 'Phone',
    value: '+1 (555) 123-4567'
  },
  {
    icon: MapPinIcon,
    label: 'Location',
    value: 'San Francisco, CA'
  }
]

const socialLinks = [
  {
    name: 'GitHub',
    url: 'https://github.com/yourusername',
    icon: 'GitHubIcon'
  },
  {
    name: 'LinkedIn',
    url: 'https://linkedin.com/in/yourusername',
    icon: 'LinkedInIcon'
  },
  {
    name: 'Twitter',
    url: 'https://twitter.com/yourusername',
    icon: 'TwitterIcon'
  }
]

const handleSubmit = async () => {
  isSubmitting.value = true
  
  // Simulate form submission
  await new Promise(resolve => setTimeout(resolve, 1500))
  
  // Reset form
  form.value = {
    name: '',
    email: '',
    message: ''
  }
  
  isSubmitting.value = false
  alert('Message sent successfully!')
}
</script>