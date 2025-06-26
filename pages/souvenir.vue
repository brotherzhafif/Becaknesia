<template>
  <div>
    <Navbar />
    <main class="min-h-screen bg-[#F7F7F7] py-20">
      <div class="max-w-6xl mx-auto px-4">
        <h1 class="text-3xl font-bold text-[#1F2937] text-center mb-12">Tempat Belanja & Souvenir</h1>
        
        <!-- Filter -->
        <div class="mb-8 flex justify-center">
          <div class="flex space-x-4">
            <button 
              v-for="category in categories" 
              :key="category"
              class="px-4 py-2 rounded font-semibold text-sm transition-colors"
              :class="selectedCategory === category ? 'bg-[#F4A800] text-white' : 'bg-white text-[#1F2937] hover:bg-[#F4A800] hover:text-white'"
              @click="selectedCategory = category"
            >
              {{ category }}
            </button>
          </div>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
          <SouvenirCard v-for="place in filteredPlaces" :key="place.id" :place="place" />
        </div>
      </div>
    </main>
    <Footer />
  </div>
</template>

<script setup>
const categories = ref(['Semua', 'Budaya', 'Ikonik', 'Kuliner', 'Alam'])
const selectedCategory = ref('Semua')
const places = ref([])
const filteredPlaces = computed(() => {
  if (selectedCategory.value === 'Semua') return places.value
  return places.value.filter(place => place.category === selectedCategory.value)
})
</script>
