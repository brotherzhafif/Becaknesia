<template>
  <section class="py-20 bg-white">
    <div class="max-w-6xl mx-auto px-4">
      <h2 class="text-3xl font-bold text-[#1F2937] text-center mb-12">Wisata & Souvenir</h2>
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
        <SouvenirCard 
          v-for="place in souvenirPlaces" 
          :key="place.id" 
          :place="place" 
        />
      </div>
    </div>
  </section>
</template>

<script setup>
const souvenirPlaces = ref([
  {
    id: 1,
    name: "Kampung Batik Ngasem",
    category: "Budaya",
    image: null
  },
  {
    id: 2,
    name: "Pasar Beringharjo", 
    category: "Ikonik",
    image: null
  },
  {
    id: 3,
    name: "Gudeg Yu Djum Wijilan",
    category: "Kuliner",
    image: null
  },
  {
    id: 4,
    name: "Sentra Kerajinan Kotagede",
    category: "Budaya", 
    image: null
  }
])
</script>
