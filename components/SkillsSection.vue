<template>
  <section id="skills" class="section bg-white">
    <div class="container">
      <h2 class="text-4xl font-bold text-center mb-16">Skills</h2>
      
      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div 
          v-for="(category, index) in skillCategories" 
          :key="index"
          v-motion
          :initial="{ opacity: 0, y: 50 }"
          :enter="{ opacity: 1, y: 0 }"
          :delay="index * 200"
          class="bg-gray-50 rounded-xl p-6"
        >
          <h3 class="text-xl font-semibold mb-6 flex items-center gap-2">
            <component :is="category.icon" class="w-6 h-6 text-primary" />
            {{ category.title }}
          </h3>
          
          <div class="space-y-4">
            <div 
              v-for="skill in category.skills" 
              :key="skill.name"
              class="relative"
            >
              <div class="flex justify-between mb-1">
                <span class="font-medium">{{ skill.name }}</span>
                <span class="text-primary">{{ skill.level }}%</span>
              </div>
              <div class="h-2 bg-gray-200 rounded-full overflow-hidden">
                <div 
                  class="h-full bg-primary transition-all duration-1000"
                  :style="{ width: '0%' }"
                  ref="progressBars"
                ></div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useIntersectionObserver } from '@vueuse/core'
import { 
  CommandLineIcon,
  CubeIcon,
  WrenchScrewdriverIcon
} from '@heroicons/vue/24/outline'

const skillCategories = [
  {
    title: 'Frontend Development',
    icon: CommandLineIcon,
    skills: [
      { name: 'Vue.js', level: 90 },
      { name: 'React', level: 85 },
      { name: 'CSS/SCSS', level: 95 },
      { name: 'JavaScript', level: 90 }
    ]
  },
  {
    title: 'Backend Development',
    icon: CubeIcon,
    skills: [
      { name: 'Node.js', level: 85 },
      { name: 'Python', level: 80 },
      { name: 'SQL', level: 85 },
      { name: 'MongoDB', level: 80 }
    ]
  },
  {
    title: 'Tools & Others',
    icon: WrenchScrewdriverIcon,
    skills: [
      { name: 'Git', level: 90 },
      { name: 'Docker', level: 75 },
      { name: 'AWS', level: 70 },
      { name: 'CI/CD', level: 80 }
    ]
  }
]

const progressBars = ref([])

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        const bar = entry.target
        const parent = bar.parentElement.parentElement
        const level = parent.querySelector('.text-primary').textContent.replace('%', '')
        gsap.to(bar, {
          width: `${level}%`,
          duration: 1,
          ease: 'power2.out'
        })
      }
    })
  }, { threshold: 0.5 })

  progressBars.value.forEach(bar => observer.observe(bar))
})
</script>