<template>
  <div class="bg-white rounded-xl shadow-md overflow-hidden hover:shadow-lg transition-shadow">
    <div class="h-48 bg-[#F7F7F7] flex items-center justify-center">
      <img :src="route.image" :alt="route.name" class="w-full h-full object-cover" v-if="route.image" />
      <Icon name="mdi:image" class="text-[#E5E7EB] text-6xl" v-else />
    </div>
    <div class="p-6">
      <h3 class="font-bold text-[#1F2937] text-xl mb-2">{{ route.name }}</h3>
      <p class="text-[#6B7280] text-sm mb-4 line-clamp-2">{{ route.description }}</p>
      <div class="flex justify-between items-center">
        <span class="font-bold text-[#009344]">{{ route.duration }}</span>
        <button class="bg-[#F4A800] hover:bg-[#e09600] text-white px-4 py-2 rounded font-semibold text-sm transition-colors">
          Detail
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  route: {
    type: Object,
    required: true
  }
})
</script>
