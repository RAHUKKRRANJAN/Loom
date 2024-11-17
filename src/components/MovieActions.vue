<script setup lang="ts">
import { ref } from 'vue'

const actions = ref([
  { 
    icon: '📋', 
    label: 'List', 
    active: false,
    options: ['Watchlist', 'Favorites', 'Custom List']
  },
  { 
    icon: '❤️', 
    label: 'Favorite', 
    active: false 
  },
  { 
    icon: '🔖', 
    label: 'Watchlist', 
    active: false 
  },
  { 
    icon: '⭐', 
    label: 'Rate', 
    active: false,
    options: ['1', '2', '3', '4', '5']
  }
])

const activeDropdown = ref<number | null>(null)

const toggleAction = (index: number) => {
  if (actions.value[index].options) {
    activeDropdown.value = activeDropdown.value === index ? null : index
  } else {
    actions.value[index].active = !actions.value[index].active
  }
}

const selectOption = (actionIndex: number, option: string) => {
  actions.value[actionIndex].active = true
  activeDropdown.value = null
}
</script>

<template>
  <div class="fixed bottom-0 left-0 right-0 bg-[#032541] border-t border-gray-700">
    <div class="flex justify-around py-4 max-w-screen-lg mx-auto px-4 relative">
      <div v-for="(action, index) in actions" 
           :key="action.label"
           class="relative">
        <button 
          @click="toggleAction(index)"
          class="flex flex-col items-center transition-transform hover:scale-110"
          :class="{ 'text-[#01b4e4]': action.active }">
          <span class="text-2xl">{{ action.icon }}</span>
          <span class="text-sm">{{ action.label }}</span>
        </button>

        <!-- Dropdown Menu -->
        <div v-if="action.options && activeDropdown === index"
             class="absolute bottom-full mb-2 bg-white rounded-lg shadow-lg py-2 w-48">
          <button v-for="option in action.options" 
                  :key="option"
                  @click="selectOption(index, option)"
                  class="w-full text-left px-4 py-2 text-gray-700 hover:bg-gray-100">
            {{ option }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>