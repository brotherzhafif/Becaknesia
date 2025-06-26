<template>
  <div>
    <Navbar />
    <div class="min-h-screen bg-[#F7F7F7] py-20">
      <div class="max-w-6xl mx-auto px-4">
        <h1 class="text-4xl font-bold text-[#1F2937] text-center mb-4">Rute Perjalanan</h1>
        <p class="text-[#6B7280] text-center mb-12 max-w-2xl mx-auto">
          Pilih paket wisata becak yang sesuai dengan minat Anda. Setiap rute dirancang untuk memberikan pengalaman budaya yang tak terlupakan.
        </p>
        
        <!-- Filter & Search -->
        <div class="mb-8 flex flex-col md:flex-row gap-4 justify-between">
          <input 
            v-model="searchQuery"
            type="text" 
            placeholder="Cari rute..." 
            class="px-4 py-2 border border-[#E5E7EB] rounded-lg focus:outline-none focus:ring-2 focus:ring-[#F4A800]"
          />
          <select 
            v-model="selectedDuration"
            class="px-4 py-2 border border-[#E5E7EB] rounded-lg focus:outline-none focus:ring-2 focus:ring-[#F4A800]"
          >
            <option value="">Semua Durasi</option>
            <option value="2-3 jam">2-3 jam</option>
            <option value="3-4 jam">3-4 jam</option>
            <option value="4-5 jam">4-5 jam</option>
          </select>
        </div>

        <!-- Route Cards -->
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <RouteCard 
            v-for="route in filteredRoutes" 
            :key="route.id" 
            :route="route"
            @click="goToDetail(route.id)"
          />
        </div>
      </div>
    </div>
    <Footer />
  </div>
</template>

<script setup>
useHead({
  title: 'Rute Perjalanan - Becaknesia',
  meta: [
    { name: 'description', content: 'Jelajahi berbagai rute wisata becak tradisional di Indonesia. Pilih paket yang sesuai dengan minat dan waktu Anda.' }
  ]
})

const searchQuery = ref('')
const selectedDuration = ref('')

const routes = ref([
  {
    id: 1,
    name: "Wisata Kraton & Taman Sari",
    description: "Jelajahi kemegahan Kraton Yogyakarta dan keindahan Taman Sari dengan becak tradisional. Nikmati cerita sejarah dari guide lokal berpengalaman.",
    duration: "3-4 jam",
    price: "Rp 75.000",
    image: null,
    includes: ["Guide lokal", "Air mineral", "Tiket masuk"]
  },
  {
    id: 2,
    name: "Malioboro & Sosrowijayan",
    description: "Nikmati suasana khas Malioboro dan gang-gang bersejarah di Sosrowijayan. Rasakan kehidupan malam kota budaya.",
    duration: "2-3 jam", 
    price: "Rp 50.000",
    image: null,
    includes: ["Guide lokal", "Snack tradisional"]
  },
  {
    id: 3,
    name: "Kampung Batik & Pasar Tradisional",
    description: "Kunjungi sentra batik dan rasakan kehidupan pasar tradisional yang autentik. Pelajari proses pembuatan batik dari pengrajin.",
    duration: "3-4 jam",
    price: "Rp 65.000",
    image: null,
    includes: ["Guide lokal", "Workshop batik", "Air mineral"]
  },
  {
    id: 4,
    name: "Kotagede Heritage Tour",
    description: "Jelajahi kawasan bersejarah Kotagede dengan kerajinan perak terkenalnya. Lihat proses pembuatan kerajinan perak tradisional.",
    duration: "4-5 jam",
    price: "Rp 85.000",
    image: null,
    includes: ["Guide lokal", "Workshop perak", "Makan siang", "Air mineral"]
  }
])

const filteredRoutes = computed(() => {
  return routes.value.filter(route => {
    const matchesSearch = route.name.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
                         route.description.toLowerCase().includes(searchQuery.value.toLowerCase())
    const matchesDuration = !selectedDuration.value || route.duration === selectedDuration.value
    return matchesSearch && matchesDuration
  })
})

const goToDetail = (routeId) => {
  navigateTo(`/rute/${routeId}`)
}
</script>
