<template>
  <section id="projects" class="section bg-gray-50">
    <div class="container">
      <h2 
        class="text-4xl font-bold text-center mb-16"
        v-motion
        :initial="{ opacity: 0, scale: 0.5 }"
        :enter="{ opacity: 1, scale: 1 }"
      >
        My Projects
      </h2>
      
      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div 
          v-for="(project, index) in projects" 
          :key="index"
          v-motion
          :initial="{ opacity: 0, y: 50 }"
          :enter="{ opacity: 1, y: 0 }"
          :delay="index * 200"
          class="group transform hover:-translate-y-2 transition-all duration-300"
          @click="openModal(project)"
        >
          <div class="bg-white rounded-xl overflow-hidden shadow-lg hover:shadow-2xl transition-all">
            <div class="relative aspect-video overflow-hidden">
              <img 
                :src="project.image" 
                :alt="project.title"
                class="w-full h-full object-cover transform group-hover:scale-110 transition-transform duration-500"
              />
              <div class="absolute inset-0 bg-primary/60 opacity-0 group-hover:opacity-100 transition-all duration-300 flex items-center justify-center">
                <span class="text-white font-semibold transform -translate-y-4 group-hover:translate-y-0 transition-transform">View Details</span>
              </div>
            </div>
            
            <div class="p-6">
              <h3 class="text-xl font-semibold mb-2 group-hover:text-primary transition-colors">{{ project.title }}</h3>
              <p class="text-gray-600 mb-4">{{ project.description }}</p>
              <div class="flex flex-wrap gap-2">
                <span 
                  v-for="tech in project.technologies" 
                  :key="tech"
                  class="px-3 py-1 bg-primary/10 text-primary rounded-full text-sm hover:bg-primary hover:text-white transition-colors"
                >
                  {{ tech }}
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Enhanced Modal -->
    <TransitionRoot appear :show="isModalOpen" as="template">
      <Dialog as="div" @close="closeModal" class="relative z-50">
        <TransitionChild
          enter="duration-300 ease-out"
          enter-from="opacity-0"
          enter-to="opacity-100"
          leave="duration-200 ease-in"
          leave-from="opacity-100"
          leave-to="opacity-0"
        >
          <div class="fixed inset-0 bg-black/70 backdrop-blur-sm" />
        </TransitionChild>

        <div class="fixed inset-0 overflow-y-auto">
          <div class="flex min-h-full items-center justify-center p-4">
            <TransitionChild
              enter="duration-300 ease-out"
              enter-from="opacity-0 scale-95 -rotate-2"
              enter-to="opacity-100 scale-100 rotate-0"
              leave="duration-200 ease-in"
              leave-from="opacity-100 scale-100 rotate-0"
              leave-to="opacity-0 scale-95 rotate-2"
            >
              <DialogPanel class="w-full max-w-3xl bg-white rounded-2xl overflow-hidden shadow-2xl transform transition-all">
                <div v-if="selectedProject" class="relative">
                  <button 
                    @click="closeModal"
                    class="absolute top-4 right-4 bg-white/80 p-2 rounded-full hover:bg-white transition-colors"
                  >
                    <XMarkIcon class="w-6 h-6" />
                  </button>
                  <img 
                    :src="selectedProject.image" 
                    :alt="selectedProject.title"
                    class="w-full aspect-video object-cover"
                  />
                  <div class="p-8">
                    <h3 class="text-2xl font-semibold mb-4">{{ selectedProject.title }}</h3>
                    <p class="text-gray-600 mb-6">{{ selectedProject.fullDescription }}</p>
                    <div class="flex flex-wrap gap-3 mb-6">
                      <span 
                        v-for="tech in selectedProject.technologies" 
                        :key="tech"
                        class="px-3 py-1 bg-primary/10 text-primary rounded-full text-sm"
                      >
                        {{ tech }}
                      </span>
                    </div>
                    <div class="flex justify-end gap-4">
                      <a 
                        v-if="selectedProject.demoUrl"
                        :href="selectedProject.demoUrl"
                        target="_blank"
                        class="btn btn-primary transform hover:scale-105 transition-transform"
                      >
                        Live Demo
                      </a>
                      <a
                        v-if="selectedProject.githubUrl"
                        :href="selectedProject.githubUrl"
                        target="_blank"
                        class="btn bg-gray-800 text-white hover:bg-gray-700 transform hover:scale-105 transition-transform"
                      >
                        View Code
                      </a>
                    </div>
                  </div>
                </div>
              </DialogPanel>
            </TransitionChild>
          </div>
        </div>
      </Dialog>
    </TransitionRoot>
  </section>
</template>

<script setup>
import { ref } from 'vue'
import {
  TransitionRoot,
  TransitionChild,
  Dialog,
  DialogPanel,
} from '@headlessui/vue'
import { XMarkIcon } from '@heroicons/vue/24/outline'

const isModalOpen = ref(false)
const selectedProject = ref(null)

const projects = [
  {
    title: 'School Management System',
    description: 'A Python-based system for managing student records',
    fullDescription: 'Developed a comprehensive school management system using Python and SQLite, featuring student attendance, grade tracking, and report generation.',
    image: '/project1.jpg',
    technologies: ['Python', 'SQLite', 'Tkinter'],
    demoUrl: 'https://demo.example.com',
    githubUrl: 'https://github.com/utkarsh/school-management'
  },
  {
    title: 'Personal Blog',
    description: 'Responsive blog website with modern design',
    fullDescription: 'Created a responsive blog website using HTML, CSS, and JavaScript with features like dark mode and comment system.',
    image: '/project2.jpg',
    technologies: ['HTML', 'CSS', 'JavaScript'],
    demoUrl: 'https://demo.example.com',
    githubUrl: 'https://github.com/utkarsh/blog'
  },
  {
    title: 'Weather App',
    description: 'Real-time weather information application',
    fullDescription: 'Built a weather application that provides real-time weather information using a weather API and modern JavaScript.',
    image: '/project3.jpg',
    technologies: ['HTML', 'CSS', 'JavaScript', 'API'],
    demoUrl: 'https://demo.example.com',
    githubUrl: 'https://github.com/utkarsh/weather-app'
  }
]

const openModal = (project) => {
  selectedProject.value = project
  isModalOpen.value = true
}

const closeModal = () => {
  isModalOpen.value = false
  setTimeout(() => {
    selectedProject.value = null
  }, 200)
}
</script>