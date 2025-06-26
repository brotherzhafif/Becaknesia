<template>
  <section class="py-20 bg-[#F7F7F7]">
    <div class="max-w-6xl mx-auto px-4">
      <h2 class="text-3xl font-bold text-[#1F2937] text-center mb-12">Rute Populer</h2>
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <RouteCard 
          v-for="route in popularRoutes" 
          :key="route.id" 
          :route="route" 
        />
      </div>
    </div>
  </section>
</template>

<script setup>
const popularRoutes = ref([
  {
    id: 1,
    name: "Wisata Kraton & Taman Sari",
    description: "Jelajahi kemegahan Kraton Yogyakarta dan keindahan Taman Sari dengan becak tradisional",
    duration: "3-4 jam",
    image: null
  },
  {
    id: 2,
    name: "Malioboro & Sosrowijayan",
    description: "Nikmati suasana khas Malioboro dan gang-gang bersejarah di Sosrowijayan",
    duration: "2-3 jam", 
    image: null
  },
  {
    id: 3,
    name: "Kampung Batik & Pasar Tradisional",
    description: "Kunjungi sentra batik dan rasakan kehidupan pasar tradisional yang autentik",
    duration: "2-3 jam",
    image: null
  }
])
</script>
