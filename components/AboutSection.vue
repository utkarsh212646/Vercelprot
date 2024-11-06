<template>
  <section id="about" class="section bg-white">
    <div class="container">
      <h2 class="text-4xl font-bold text-center mb-16">About Me</h2>
      
      <div class="grid md:grid-cols-2 gap-12 items-center">
        <div 
          class="relative group"
          v-motion
          :initial="{ opacity: 0, x: -50 }"
          :enter="{ opacity: 1, x: 0 }"
        >
          <div class="aspect-square rounded-2xl overflow-hidden transform group-hover:scale-105 transition-transform duration-500">
            <img
              src="/placeholder-profile.jpg"
              alt="Utkarsh Dubey"
              class="w-full h-full object-cover"
            />
          </div>
          <div class="absolute inset-0 bg-primary/10 rounded-2xl transform rotate-6 -z-10 group-hover:rotate-12 transition-transform"></div>
        </div>
        
        <div
          v-motion
          :initial="{ opacity: 0, x: 50 }"
          :enter="{ opacity: 1, x: 0 }"
        >
          <h3 class="text-2xl font-semibold mb-4">Utkarsh Dubey</h3>
          <p class="text-gray-600 mb-6">
            A young and passionate developer with a strong foundation in HTML, Java, CSS, and Python.
            Currently in Class 10, I've already completed over 60 paid projects, showcasing my dedication
            to web development and problem-solving.
          </p>
          
          <div class="space-y-4">
            <div v-for="(item, index) in achievements" :key="index" class="flex gap-4 group hover:transform hover:translate-x-2 transition-transform">
              <div class="w-12 h-12 rounded-full bg-primary/10 flex items-center justify-center shrink-0 group-hover:bg-primary/20 transition-colors">
                <component :is="item.icon" class="w-6 h-6 text-primary" />
              </div>
              <div>
                <h4 class="font-semibold">{{ item.title }}</h4>
                <p class="text-sm text-gray-600">{{ item.description }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { 
  AcademicCapIcon, 
  TrophyIcon,
  CodeBracketIcon 
} from '@heroicons/vue/24/outline'

const achievements = [
  {
    title: '60+ Projects Completed',
    description: 'Successfully delivered various web development projects',
    icon: TrophyIcon
  },
  {
    title: 'Student Developer',
    description: 'Class 10 student with passion for coding',
    icon: AcademicCapIcon
  },
  {
    title: 'Tech Stack',
    description: 'Proficient in HTML, Java, CSS, and Python',
    icon: CodeBracketIcon
  }
]
</script>