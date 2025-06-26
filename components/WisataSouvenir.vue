<template>
  <section class="py-20 bg-white">
    <div class="max-w-6xl mx-auto px-4">
      <h2 class="text-3xl font-bold text-[#1F2937] text-center mb-12">Wisata & Souvenir</h2>
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
        <SouvenirCard 
          v-for="place in souvenirPlaces" 
          :key="place._id" 
          :place="place" 
        />
      </div>
      <div class="text-center mt-8">
        <NuxtLink 
          to="/souvenir"
          class="bg-[#F4A800] hover:bg-[#e09600] text-white px-6 py-2 rounded font-semibold transition-colors"
        >
          Lihat Semua
        </NuxtLink>
      </div>
    </div>
  </section>
</template>

<script setup>
const API_BASE = 'http://70.153.72.39:8011'

const souvenirPlaces = ref([])
const loading = ref(false)

// Fetch places from API
const fetchSouvenirPlaces = async () => {
  loading.value = true
  try {
    const response = await $fetch(`${API_BASE}/place/`, {
      query: {
        page: 1,
        limit: 4 // Only get 4 places for preview
      }
    })
    
    if (response.status === 'success') {
      souvenirPlaces.value = response.data.data || []
    }
  } catch (error) {
    console.error('Failed to fetch souvenir places:', error)
    // Fallback to static data if API fails
    souvenirPlaces.value = [
      {
        _id: 1,
        name: "Kampung Batik Ngasem",
        category: "Budaya",
        photo: null
      },
      {
        _id: 2,
        name: "Pasar Beringharjo", 
        category: "Ikonik",
        photo: null
      },
      {
        _id: 3,
        name: "Gudeg Yu Djum Wijilan",
        category: "Kuliner",
        photo: null
      },
      {
        _id: 4,
        name: "Sentra Kerajinan Kotagede",
        category: "Budaya", 
        photo: null
      }
    ]
  } finally {
    loading.value = false
  }
}

// Fetch data on component mount
onMounted(() => {
  fetchSouvenirPlaces()
})
</script>
