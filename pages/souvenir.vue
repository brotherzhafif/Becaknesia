<template>
  <div>
    <Navbar />
    <main class="min-h-screen bg-[#F7F7F7] py-20">
      <div class="max-w-6xl mx-auto px-4">
        <h1 class="text-3xl font-bold text-[#1F2937] text-center mb-12">Tempat Belanja & Souvenir</h1>
        
        <!-- Search & Filter -->
        <div class="mb-8 flex flex-col md:flex-row gap-4 justify-between">
          <div class="flex-1 max-w-md">
            <input 
              type="text" 
              v-model="searchQuery"
              @input="searchPlaces"
              placeholder="Cari tempat..." 
              class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-[#F4A800]"
            />
          </div>
          <div class="flex gap-2">
            <select 
              v-model="currentLimit" 
              @change="fetchPlaces"
              class="px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-[#F4A800]"
            >
              <option value="8">8 per halaman</option>
              <option value="16">16 per halaman</option>
              <option value="32">32 per halaman</option>
            </select>
          </div>
        </div>

        <!-- Loading State -->
        <div v-if="loading" class="text-center py-12">
          <Icon name="mdi:loading" class="text-4xl animate-spin text-[#F4A800]" />
          <p class="mt-2 text-[#6B7280]">Memuat tempat...</p>
        </div>

        <!-- Places Grid -->
        <div v-else-if="places.length > 0" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
          <SouvenirCard v-for="place in places" :key="place._id" :place="place" />
        </div>

        <!-- Empty State -->
        <div v-else class="text-center py-12">
          <Icon name="mdi:store-search" class="text-6xl text-[#E5E7EB] mb-4" />
          <h3 class="text-xl font-semibold text-[#1F2937] mb-2">Tidak ada tempat ditemukan</h3>
          <p class="text-[#6B7280]">Coba gunakan kata kunci pencarian yang berbeda</p>
        </div>

        <!-- Pagination -->
        <div v-if="totalPages > 1" class="mt-12 flex justify-center">
          <div class="flex space-x-2">
            <button 
              @click="goToPage(currentPage - 1)"
              :disabled="currentPage === 1"
              class="px-4 py-2 border border-gray-300 rounded-lg disabled:opacity-50 disabled:cursor-not-allowed hover:bg-[#F4A800] hover:text-white transition-colors"
            >
              Sebelumnya
            </button>
            
            <button 
              v-for="page in visiblePages" 
              :key="page"
              @click="goToPage(page)"
              :class=" [
                'px-4 py-2 border border-gray-300 rounded-lg transition-colors',
                currentPage === page ? 'bg-[#F4A800] text-white' : 'hover:bg-[#F4A800] hover:text-white'
              ]"
            >
              {{ page }}
            </button>
            
            <button 
              @click="goToPage(currentPage + 1)"
              :disabled="currentPage === totalPages"
              class="px-4 py-2 border border-gray-300 rounded-lg disabled:opacity-50 disabled:cursor-not-allowed hover:bg-[#F4A800] hover:text-white transition-colors"
            >
              Selanjutnya
            </button>
          </div>
        </div>
      </div>
    </main>
    <Footer />
  </div>
</template>

<script setup>
const API_BASE = 'http://70.153.72.39:8011'

const places = ref([])
const loading = ref(false)
const searchQuery = ref('')
const currentPage = ref(1)
const currentLimit = ref(8)
const totalPages = ref(1)
const total = ref(0)

let searchTimeout = null

// Fetch places from API
const fetchPlaces = async () => {
  loading.value = true
  try {
    const response = await $fetch(`${API_BASE}/place/`, {
      query: {
        page: currentPage.value,
        limit: currentLimit.value,
        search: searchQuery.value || undefined
      }
    })
    
    if (response.status === 'success') {
      places.value = response.data.data || []
      currentPage.value = response.data.page || 1
      totalPages.value = response.data.totalPages || 1
      total.value = response.data.total || 0
    }
  } catch (error) {
    console.error('Failed to fetch places:', error)
  } finally {
    loading.value = false
  }
}

// Search places with debounce
const searchPlaces = () => {
  clearTimeout(searchTimeout)
  searchTimeout = setTimeout(() => {
    currentPage.value = 1
    fetchPlaces()
  }, 500)
}

// Go to specific page
const goToPage = (page) => {
  if (page >= 1 && page <= totalPages.value) {
    currentPage.value = page
    fetchPlaces()
  }
}

// Calculate visible page numbers
const visiblePages = computed(() => {
  const pages = []
  const start = Math.max(1, currentPage.value - 2)
  const end = Math.min(totalPages.value, start + 4)
  
  for (let i = start; i <= end; i++) {
    pages.push(i)
  }
  
  return pages
})

// Fetch data on component mount
onMounted(() => {
  fetchPlaces()
})
</script>
