<script setup>
import { ref, toRefs } from 'vue'
import { useMovieStore } from '../stores/movie'
import { storeToRefs } from 'pinia'
import 'vue3-carousel/dist/carousel.css'
import { Carousel, Slide, Navigation } from 'vue3-carousel'
const useMovie = useMovieStore()
const { movie, showFullVideo } = storeToRefs(useMovie)

let currentSlide = ref(0)

const props = defineProps({
  category: String,
  movies: Array
})
const { category, movies } = toRefs(props)

const currentSlideObject = (slide, index) => {
  if (index === currentSlide.value) {
    movie.value = slide
  }
}
const fullScreenVideo = (index) => {
  currentSlide.value = index
  setTimeout(() => (showFullVideo.value = true), 500)
}
</script>
<template>
  <div class="relative min-w-[1200px]">
    <div class="flex justify-between mr-6">
      <div class="flex item-center font-semibold text-white text-2xl cursor-pointer">
        {{ category }}
      </div>
    </div>
    <Carousel
      ref="carousel"
      v-model="currentSlide"
      :items-to-show="8"
      :items-to-scroll="1"
      :wrap-around="true"
      :transition="500"
      snap-align="start"
      class="bg-transparent"
    >
      <Slide
        v-for="(slide, index) in movies"
        :key="slide"
        class="bg-transparent text-white flex items-center object-cover"
      >
        <div
          @click="fullScreenVideo(index)"
          class="object-cover h-full hover:brightness-100 cursor-pointer"
          :class="[
            currentSlide !== index ? 'border-4 border-transparent' : 'border-4 border-white',
            currentSlideObject(slide, index)
          ]"
        >
          <img
            :src="'/images/' + slide?.name + '.png'"
            :alt="slide?.name"
            class="pointer-events-none h-full z-[-1]"
          />
        </div>
      </Slide>
      <template #addons>
        <Navigation />
      </template>
    </Carousel>
  </div>
</template>
<style>
.carousel__prev,
.carousel__next,
.carousel__prev:hover,
.carousel__next:hover {
  color: white;
}
</style>
