<template>
  <footer class="bg-gray-900 text-white py-12">
    <div class="container mx-auto px-4">
      <div class="grid md:grid-cols-3 gap-8">
        <div>
          <h3 class="text-xl font-bold mb-4">Your Name</h3>
          <p class="text-gray-400">
            Building amazing web experiences with modern technologies.
          </p>
        </div>
        
        <div>
          <h3 class="text-xl font-bold mb-4">Quick Links</h3>
          <ul class="space-y-2">
            <li v-for="link in quickLinks" :key="link.href">
              <a 
                :href="link.href"
                class="text-gray-400 hover:text-white transition-colors"
              >
                {{ link.label }}
              </a>
            </li>
          </ul>
        </div>
        
        <div>
          <h3 class="text-xl font-bold mb-4">Connect</h3>
          <div class="flex gap-4">
            <a 
              v-for="social in socialLinks" 
              :key="social.name"
              :href="social.url"
              target="_blank"
              class="text-gray-400 hover:text-white transition-colors"
            >
              <component :is="social.icon" class="w-6 h-6" />
            </a>
          </div>
        </div>
      </div>
      
      <div class="border-t border-gray-800 mt-8 pt-8 text-center text-gray-400">
        <p>&copy; {{ new Date().getFullYear() }} Your Name. All rights reserved.</p>
      </div>
    </div>
  </footer>
</template>

<script setup>
const quickLinks = [
  { label: 'Home', href: '#home' },
  { label: 'About', href: '#about' },
  { label: 'Projects', href: '#projects' },
  { label: 'Skills<boltAction type="file" filePath="components/FooterSection.vue">', href: '#skills' },
  { label: 'Contact', href: '#contact' }
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
</script>