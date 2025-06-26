<template>
  <div>
    <Navbar />
    <div class="min-h-screen bg-white py-20">
      <div class="max-w-6xl mx-auto px-4">
        <h1 class="text-4xl font-bold text-[#1F2937] text-center mb-4">Souvenir & Wisata Belanja</h1>
        <p class="text-[#6B7280] text-center mb-12 max-w-2xl mx-auto">
          Temukan tempat-tempat terbaik untuk berbelanja souvenir dan produk lokal khas Indonesia. Dukung UMKM lokal dengan berbelanja di tempat-tempat autentik.
        </p>

        <!-- Categories -->
        <div class="flex flex-wrap justify-center gap-4 mb-8">
          <button 
            v-for="category in categories"
            :key="category"
            @click="selectedCategory = category"
            :class=" [
              'px-6 py-2 rounded-full transition-colors',
              selectedCategory === category 
                ? 'bg-[#F4A800] text-white' 
                : 'bg-[#F7F7F7] text-[#6B7280] hover:bg-[#E5E7EB]'
            ]"
          >
            {{ category }}
          </button>
        </div>

        <!-- Places Grid -->
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <SouvenirCard 
            v-for="place in filteredPlaces" 
            :key="place.id" 
            :place="place" 
          />
        </div>
      </div>
    </div>
    <Footer />
  </div>
</template>

<script setup>
useHead({
  title: 'Souvenir & Wisata Belanja - Becaknesia',
  meta: [
    { name: 'description', content: 'Temukan tempat-tempat terbaik untuk berbelanja souvenir dan produk lokal khas Indonesia. Dukung UMKM dan ekonomi lokal.' }
  ]
})

const selectedCategory = ref('Semua')

const categories = ['Semua', 'Budaya', 'Kuliner', 'Kerajinan', 'Fashion', 'Ikonik']

const places = ref([
  {
    id: 1,
    name: "Kampung Batik Ngasem",
    category: "Budaya",
    description: "Pusat kerajinan batik tradisional dengan beragam motif khas Yogyakarta",
    address: "Ngasem, Kraton, Yogyakarta",
    openHours: "08:00 - 17:00",
    image: null,
    specialties: ["Batik Tulis", "Batik Cap", "Kain Jumputan"]
  },
  {
    id: 2,
    name: "Pasar Beringharjo", 
    category: "Ikonik",
    description: "Pasar tradisional tertua di Yogyakarta dengan berbagai produk lokal",
    address: "Jl. Ahmad Yani, Ngupasan, Gondomanan",
    openHours: "06:00 - 16:00",
    image: null,
    specialties: ["Batik", "Jamu", "Makanan Tradisional", "Souvenir"]
  },
  {
    id: 3,
    name: "Gudeg Yu Djum Wijilan",
    category: "Kuliner",
    description: "Warung gudeg legendaris dengan cita rasa autentik Yogyakarta",
    address: "Jl. Wijilan No.167, Panembahan",
    openHours: "06:00 - 12:00",
    image: null,
    specialties: ["Gudeg Jogja", "Ayam Kampung", "Telur Pindang"]
  },
  {
    id: 4,
    name: "Sentra Kerajinan Kotagede",
    category: "Kerajinan", 
    description: "Pusat kerajinan perak terkenal dengan kualitas tinggi dan motif tradisional",
    address: "Kotagede, Bantul, Yogyakarta",
    openHours: "09:00 - 17:00",
    image: null,
    specialties: ["Kerajinan Perak", "Perhiasan", "Miniatur", "Souvenir Perak"]
  },
  {
    id: 5,
    name: "Malioboro Street",
    category: "Fashion",
    description: "Jalan paling terkenal di Yogyakarta dengan toko-toko fashion dan souvenir",
    address: "Jl. Malioboro, Sosromenduran",
    openHours: "24 Jam",
    image: null,
    specialties: ["Kaos Jogja", "Aksesoris", "Souvenir", "Fashion Lokal"]
  },
  {
    id: 6,
    name: "Toko Pia Pathok 25",
    category: "Kuliner",
    description: "Toko pia legendaris dengan berbagai varian rasa khas Yogyakarta",
    address: "Jl. KH Ahmad Dahlan No.25",
    openHours: "08:00 - 20:00",
    image: null,
    specialties: ["Pia Jogja", "Pia Keju", "Pia Coklat", "Oleh-oleh Khas"]
  }
])

const filteredPlaces = computed(() => {
  if (selectedCategory.value === 'Semua') {
    return places.value
  }
  return places.value.filter(place => place.category === selectedCategory.value)
})
</script>
