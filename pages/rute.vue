<template>
  <div>
    <Navbar />
    <main class="min-h-screen bg-[#F7F7F7] py-20">
      <div class="max-w-6xl mx-auto px-4">
        <h1 class="text-3xl font-bold text-[#1F2937] text-center mb-12">Rute Perjalanan Wisata</h1>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <RouteCard v-for="route in routes" :key="route.id" :route="route" />
        </div>
      </div>
    </main>
    <Footer />
  </div>
</template>

<script setup>
const routes = ref([
  // Add route data here
])
</script>
