<template>
  <div class="bg-white rounded-xl shadow-md overflow-hidden hover:shadow-lg transition-shadow relative">
    <button class="absolute top-4 right-4 bg-[#F4A800] hover:bg-[#e09600] text-white px-3 py-1 rounded text-xs font-semibold transition-colors z-10">
      Lihat
    </button>
    <div class="h-48 bg-[#F7F7F7] flex items-center justify-center">
      <img :src="place.image" :alt="place.name" class="w-full h-full object-cover" v-if="place.image" />
      <Icon name="mdi:store" class="text-[#E5E7EB] text-6xl" v-else />
    </div>
    <div class="p-6">
      <h3 class="font-bold text-[#1F2937] text-lg mb-2">{{ place.name }}</h3>
      <span class="inline-block bg-[#F4A800] text-white px-2 py-1 rounded text-xs font-semibold">
        {{ place.category }}
      </span>
    </div>
  </div>
</template>

<script setup>
defineProps({
  place: {
    type: Object,
    required: true
  }
})
</script>
