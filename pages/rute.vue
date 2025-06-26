<template>
  <div>
    <Navbar />
    <main class="min-h-screen bg-[#F7F7F7] py-20">
      <div class="max-w-6xl mx-auto px-4">
        <h1 class="text-3xl font-bold text-[#1F2937] text-center mb-12">Rute Perjalanan Wisata</h1>
        
        <!-- Search & Filter -->
        <div class="mb-8 flex flex-col md:flex-row gap-4 justify-between">
          <div class="flex-1 max-w-md">
            <input 
              type="text" 
              v-model="searchQuery"
              @input="searchRoutes"
              placeholder="Cari rute wisata..." 
              class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-[#F4A800]"
            />
          </div>
          <div class="flex gap-2">
            <select 
              v-model="currentLimit" 
              @change="fetchRoutes"
              class="px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-[#F4A800]"
            >
              <option value="6">6 per halaman</option>
              <option value="12">12 per halaman</option>
              <option value="24">24 per halaman</option>
            </select>
          </div>
        </div>

        <!-- Loading State -->
        <div v-if="loading" class="text-center py-12">
          <Icon name="mdi:loading" class="text-4xl animate-spin text-[#F4A800]" />
          <p class="mt-2 text-[#6B7280]">Memuat rute...</p>
        </div>

        <!-- Routes Grid -->
        <div v-else-if="routes.length > 0" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <RouteCard v-for="route in routes" :key="route._id" :route="route" />
        </div>

        <!-- Empty State -->
        <div v-else class="text-center py-12">
          <Icon name="mdi:map-search" class="text-6xl text-[#E5E7EB] mb-4" />
          <h3 class="text-xl font-semibold text-[#1F2937] mb-2">Tidak ada rute ditemukan</h3>
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

const routes = ref([])
const loading = ref(false)
const searchQuery = ref('')
const currentPage = ref(1)
const currentLimit = ref(6)
const totalPages = ref(1)
const total = ref(0)

let searchTimeout = null

// Fetch routes from API
const fetchRoutes = async () => {
  loading.value = true
  try {
    const response = await $fetch(`${API_BASE}/tour/`, {
      query: {
        page: currentPage.value,
        limit: currentLimit.value,
        search: searchQuery.value || undefined
      }
    })
    
    if (response.status === 'success') {
      routes.value = response.data.data || []
      currentPage.value = response.data.page || 1
      totalPages.value = response.data.totalPages || 1
      total.value = response.data.total || 0
    }
  } catch (error) {
    console.error('Failed to fetch routes:', error)
  } finally {
    loading.value = false
  }
}

// Search routes with debounce
const searchRoutes = () => {
  clearTimeout(searchTimeout)
  searchTimeout = setTimeout(() => {
    currentPage.value = 1
    fetchRoutes()
  }, 500)
}

// Go to specific page
const goToPage = (page) => {
  if (page >= 1 && page <= totalPages.value) {
    currentPage.value = page
    fetchRoutes()
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
  fetchRoutes()
})
</script>
