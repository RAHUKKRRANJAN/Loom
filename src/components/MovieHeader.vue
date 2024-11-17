<script setup lang="ts">
import { ref } from 'vue'

const isMenuOpen = ref(false)
const activeDropdown = ref<string | null>(null)

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
  activeDropdown.value = null
}

const toggleDropdown = (menu: string) => {
  activeDropdown.value = activeDropdown.value === menu ? null : menu
}

const menus = {
  overview: [
    { label: 'Main', link: '#' },
    { label: 'Alternative Titles', link: '#' },
    { label: 'Cast & Crew', link: '#' },
    { label: 'Release Dates', link: '#' },
    { label: 'Translations', link: '#' }
  ],
  media: [
    { label: 'Backdrops', count: 46 },
    { label: 'Logos', count: 8 },
    { label: 'Posters', count: 123 },
    { label: 'Videos', count: 15 }
  ],
  fandom: [
    { label: 'Discussions', count: 24 },
    { label: 'Reviews', count: 12 },
    { label: 'Ratings', count: '2.4k' }
  ],
  share: [
    { label: 'Share on Facebook', icon: '📱' },
    { label: 'Share on Twitter', icon: '🐦' },
    { label: 'Copy Link', icon: '🔗' }
  ]
}
</script>

<template>
  <header class="bg-[#032541] p-4 relative">
    <div class="flex justify-between items-center">
      <div class="flex items-center gap-4">
        <button @click="toggleMenu" class="text-white md:hidden">☰</button>
        <img src="https://www.themoviedb.org/assets/2/v4/logos/v2/blue_short-8e7b30f73a4020692ccca9c88bafe5dcb6f8a62a4c6bc55cd9ba82bb2cd95f6c.svg" 
             alt="TMDB Logo" 
             class="h-5" />
      </div>
      <div class="flex items-center gap-4">
        <span class="cursor-pointer">👤</span>
        <span class="cursor-pointer">🔍</span>
      </div>
    </div>
    
    <nav :class="['bg-[#032541] border-b border-gray-700 relative', isMenuOpen ? 'block' : 'hidden md:block']">
      <div class="flex flex-col md:flex-row gap-4 md:gap-8 px-4 py-2">
        <div v-for="(items, menu) in menus" :key="menu" class="relative">
          <button 
            @click="toggleDropdown(menu)"
            class="text-white font-semibold text-left capitalize w-full md:w-auto"
            :class="{ 'text-[#01b4e4]': activeDropdown === menu }">
            {{ menu }} ▼
          </button>
          
          <div v-if="activeDropdown === menu"
               class="absolute left-0 mt-2 w-64 bg-white rounded-lg shadow-lg py-2 z-50">
            <template v-if="menu === 'media'">
              <a v-for="item in items" :key="item.label"
                 href="#" 
                 class="flex items-center justify-between px-4 py-2 text-gray-700 hover:bg-gray-100">
                <span>{{ item.label }}</span>
                <span class="bg-gray-200 px-2 rounded-full text-sm">{{ item.count }}</span>
              </a>
            </template>
            <template v-else-if="menu === 'share'">
              <a v-for="item in items" :key="item.label"
                 href="#"
                 class="flex items-center gap-2 px-4 py-2 text-gray-700 hover:bg-gray-100">
                <span>{{ item.icon }}</span>
                <span>{{ item.label }}</span>
              </a>
            </template>
            <template v-else>
              <a v-for="item in items" :key="item.label"
                 href="#"
                 class="block px-4 py-2 text-gray-700 hover:bg-gray-100">
                {{ item.label }}
                <span v-if="item.count" class="ml-2 text-gray-500">({{ item.count }})</span>
              </a>
            </template>
          </div>
        </div>
      </div>
    </nav>
  </header>
</template>

<style scoped>
.dropdown-enter-active,
.dropdown-leave-active {
  transition: all 0.3s ease;
}

.dropdown-enter-from,
.dropdown-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
</style>