<script setup>
defineProps({
  movie: Object
})
</script>
<template>
  <div class="z-40 text-white w-[53%] pt-20">
    <div class="fond-semibold fond-serif text-[55px]">
      {{ movie?.name }}
    </div>
    <div class="flex items-center text-lg pt-4">
      <div>{{ movie?.year }}</div>
      <div class="relative">
        <span class="absolute left-[2px] -top-[12px] text-[40px]">.</span>
        <span class="pl-4">{{ movie?.genre.one }}</span>
      </div>
      <div class="relative">
        <span class="absolute left-[2px] -top-[12px] text-[40px]">.</span>
        <span class="pl-4">{{ movie?.genre.two }}</span>
      </div>
      <div class="relative">
        <span class="absolute left-[2px] -top-[12px] text-[40px]">.</span>
        <span class="pl-4">{{ movie?.genre.three }}</span>
      </div>
    </div>
    <div class="pt-6 text-2xl">
      {{ movie?.description }}
    </div>
  </div>
</template>
