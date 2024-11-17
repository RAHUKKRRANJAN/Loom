<script setup lang="ts">
import MovieHeader from './components/MovieHeader.vue'
import MovieHero from './components/MovieHero.vue'
import MovieActions from './components/MovieActions.vue'

const movieData = {
  title: 'Guardians of the Galaxy Vol. 2',
  year: '2017',
  userScore: 76,
  releaseDate: '05/02/2017 (KR)',
  runtime: '2h 17m',
  genres: ['Adventure', 'Action', 'Science Fiction'],
  tagline: 'Obviously.',
  overview: 'The Guardians must fight to keep their newfound family together as they unravel the mysteries of Peter Quill\'s true parentage.'
}
</script>

<template>
  <div class="min-h-screen bg-[#032541] text-white">
    <MovieHeader />
    <MovieHero :movie="movieData" />
    <MovieActions />
  </div>
</template>