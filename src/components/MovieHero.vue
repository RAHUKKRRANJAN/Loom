<script setup lang="ts">
import { ref } from 'vue'

defineProps<{
  movie: {
    title: string
    year: string
    userScore: number
    releaseDate: string
    runtime: string
    genres: string[]
    tagline: string
    overview: string
  }
}>()

const showTrailer = ref(false)

const playTrailer = () => {
  showTrailer.value = true
}

const closeTrailer = () => {
  showTrailer.value = false
}
</script>

<template>
  <div class="relative">
    <div class="absolute inset-0 bg-gradient-to-r from-[#032541] to-transparent"></div>
    <div class="relative z-10 flex flex-col md:flex-row gap-8 p-4 md:p-8">
      <img src="https://image.tmdb.org/t/p/w300/y4MBh0EjBlMuOzv9axM4qJlmhzz.jpg" 
           alt="Movie Poster" 
           class="rounded-lg w-48 md:w-64 mx-auto md:mx-0" />
      
      <div class="flex flex-col gap-4">
        <div>
          <h1 class="text-2xl md:text-4xl font-bold text-center md:text-left">
            {{ movie.title }} <span class="font-normal">({{ movie.year }})</span>
          </h1>
          <div class="flex flex-col md:flex-row items-center gap-4 mt-4">
            <div class="flex items-center gap-2">
              <div class="relative">
                <div class="w-16 h-16 rounded-full bg-[#081c22] flex items-center justify-center border-4 border-green-500">
                  <span class="text-white font-bold text-xl">{{ movie.userScore }}%</span>
                </div>
              </div>
              <span class="font-bold">User Score</span>
            </div>
            <button 
              @click="playTrailer"
              class="bg-[#032541] px-4 py-2 rounded-full hover:bg-[#0c4a6e] transition-colors">
              ▶ Play Trailer
            </button>
          </div>
        </div>

        <div class="text-sm text-center md:text-left">
          <span>{{ movie.releaseDate }}</span>
          <span> • </span>
          <span>{{ movie.runtime }}</span>
        </div>

        <div class="flex flex-wrap gap-2 justify-center md:justify-start">
          <span v-for="genre in movie.genres" :key="genre" class="bg-[#0c4a6e] px-3 py-1 rounded-full text-sm">
            {{ genre }}
          </span>
        </div>

        <div class="text-center md:text-left">
          <p class="italic text-lg">{{ movie.tagline }}</p>
          <h3 class="text-xl font-bold mt-4">Overview</h3>
          <p class="mt-2">{{ movie.overview }}</p>
        </div>
      </div>
    </div>

    <!-- Trailer Modal -->
    <div v-if="showTrailer" 
         class="fixed inset-0 bg-black bg-opacity-75 z-50 flex items-center justify-center p-4">
      <div class="bg-[#032541] p-4 rounded-lg w-full max-w-4xl">
        <div class="flex justify-between items-center mb-4">
          <h3 class="text-xl font-bold">Official Trailer</h3>
          <button @click="closeTrailer" class="text-2xl">&times;</button>
        </div>
        <div class="relative pt-[56.25%]">
          <iframe 
            class="absolute inset-0 w-full h-full"
            src="https://www.youtube.com/embed/wUn05hdkhjM"
            allowfullscreen>
          </iframe>
        </div>
      </div>
    </div>
  </div>
</template>