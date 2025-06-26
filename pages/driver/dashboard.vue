<template>
  <div class="min-h-screen bg-[#F7F7F7]">
    <!-- Driver Header -->
    <header class="bg-[#009344] text-white py-4">
      <div class="max-w-6xl mx-auto px-4 flex justify-between items-center">
        <h1 class="text-xl font-bold">Driver Dashboard</h1>
        <button class="text-sm hover:text-[#F4A800]">Logout</button>
      </div>
    </header>

    <main class="max-w-4xl mx-auto px-4 py-8">
      <!-- Driver Stats -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8">
        <div class="bg-white rounded-lg shadow-md p-6">
          <div class="flex items-center justify-between">
            <div>
              <p class="text-[#6B7280] text-sm">Order Hari Ini</p>
              <p class="text-2xl font-bold text-[#1F2937]">3</p>
            </div>
            <Icon name="mdi:calendar-today" class="text-[#F4A800] text-4xl" />
          </div>
        </div>
        
        <div class="bg-white rounded-lg shadow-md p-6">
          <div class="flex items-center justify-between">
            <div>
              <p class="text-[#6B7280] text-sm">Rating</p>
              <p class="text-2xl font-bold text-[#1F2937]">4.8</p>
            </div>
            <Icon name="mdi:star" class="text-[#F4A800] text-4xl" />
          </div>
        </div>
      </div>

      <!-- Order List -->
      <div class="bg-white rounded-lg shadow-md p-6 mb-6">
        <h2 class="text-xl font-bold text-[#1F2937] mb-4">Order Masuk</h2>
        <div class="space-y-4">
          <div class="border border-[#E5E7EB] rounded-lg p-4">
            <div class="flex justify-between items-start mb-2">
              <div>
                <h3 class="font-medium text-[#1F2937]">Kraton & Taman Sari</h3>
                <p class="text-sm text-[#6B7280]">John Doe • 2 orang</p>
              </div>
              <span class="bg-[#F4A800] text-white px-2 py-1 rounded text-xs">Baru</span>
            </div>
            <p class="text-sm text-[#6B7280] mb-3">Pickup: Jl. Malioboro No. 123</p>
            <div class="flex space-x-2">
              <button class="bg-[#009344] hover:bg-[#006B34] text-white px-4 py-2 rounded text-sm transition-colors">
                Terima
              </button>
              <button class="border border-[#E5E7EB] text-[#6B7280] hover:bg-[#F7F7F7] px-4 py-2 rounded text-sm transition-colors">
                Tolak
              </button>
            </div>
          </div>
        </div>
      </div>

      <!-- Recent Reviews -->
      <div class="bg-white rounded-lg shadow-md p-6">
        <h2 class="text-xl font-bold text-[#1F2937] mb-4">Ulasan Terbaru</h2>
        <div class="space-y-4">
          <div class="border-b border-[#E5E7EB] pb-4">
            <div class="flex items-center space-x-2 mb-2">
              <span class="font-medium text-[#1F2937]">Jane Smith</span>
              <div class="flex text-[#F4A800]">
                <Icon name="mdi:star" v-for="n in 5" :key="n" />
              </div>
            </div>
            <p class="text-sm text-[#6B7280]">Driver sangat ramah dan berpengetahuan luas tentang sejarah Yogyakarta.</p>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>
