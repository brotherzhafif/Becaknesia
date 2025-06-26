<template>
  <div class="bg-white rounded-xl shadow-md overflow-hidden hover:shadow-lg transition-shadow">
    <div class="h-48 bg-[#F7F7F7] flex items-center justify-center">
      <img :src="route.photo" :alt="route.route_name" class="w-full h-full object-cover" v-if="route.photo" />
      <Icon name="mdi:image" class="text-[#E5E7EB] text-6xl" v-else />
    </div>
    <div class="p-6">
      <h3 class="font-bold text-[#1F2937] text-xl mb-2">{{ route.route_name || route.name }}</h3>
      <p class="text-[#6B7280] text-sm mb-4 line-clamp-2">{{ route.description }}</p>
      <div class="flex justify-between items-center">
        <span class="font-bold text-[#009344]">{{ formatDuration(route.duration) }}</span>
        <div class="flex items-center space-x-2">
          <span class="text-lg font-bold text-[#009344]" v-if="route.prices">
            Rp {{ formatPrice(route.prices) }}
          </span>
          <NuxtLink 
            :to="`/rute/${route._id}`"
            class="bg-[#F4A800] hover:bg-[#e09600] text-white px-4 py-2 rounded font-semibold text-sm transition-colors"
          >
            Detail
          </NuxtLink>
        </div>
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

// Format duration from number to readable string
const formatDuration = (duration) => {
  if (typeof duration === 'string') return duration
  if (typeof duration === 'number') {
    return duration >= 60 ? `${Math.floor(duration / 60)} hari` : `${duration} jam`
  }
  return 'Durasi tidak tersedia'
}

// Format price to IDR format
const formatPrice = (price) => {
  return new Intl.NumberFormat('id-ID').format(price)
}
</script>
