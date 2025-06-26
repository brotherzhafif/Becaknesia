<template>
  <section class="py-20 bg-[#F7F7F7]">
    <div class="max-w-6xl mx-auto px-4">
      <h2 class="text-3xl font-bold text-[#1F2937] text-center mb-12">Rute Populer</h2>
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <RouteCard 
          v-for="route in popularRoutes" 
          :key="route._id" 
          :route="route" 
        />
      </div>
    </div>
  </section>
</template>

<script setup>
const API_BASE = 'http://70.153.72.39:8011'

const popularRoutes = ref([])
const loading = ref(false)

// Fetch popular tours from API
const fetchPopularRoutes = async () => {
  loading.value = true
  try {
    const response = await $fetch(`${API_BASE}/tour/`, {
      query: {
        page: 1,
        limit: 3 // Only get 3 popular routes
      }
    })
    
    if (response.status === 'success') {
      popularRoutes.value = response.data.data || []
    }
  } catch (error) {
    console.error('Failed to fetch popular routes:', error)
    // Fallback to static data if API fails
    popularRoutes.value = [
      {
        _id: 1,
        route_name: "Wisata Kraton & Taman Sari",
        description: "Jelajahi kemegahan Kraton Yogyakarta dan keindahan Taman Sari dengan becak tradisional",
        duration: "3-4 jam",
        photo: null
      },
      {
        _id: 2,
        route_name: "Malioboro & Sosrowijayan",
        description: "Nikmati suasana khas Malioboro dan gang-gang bersejarah di Sosrowijayan",
        duration: "2-3 jam", 
        photo: null
      },
      {
        _id: 3,
        route_name: "Kampung Batik & Pasar Tradisional",
        description: "Kunjungi sentra batik dan rasakan kehidupan pasar tradisional yang autentik",
        duration: "2-3 jam",
        photo: null
      }
    ]
  } finally {
    loading.value = false
  }
}

// Fetch data on component mount
onMounted(() => {
  fetchPopularRoutes()
})
</script>
