<template>
  <nav class="bg-[#009344] shadow-lg">
    <div class="max-w-6xl mx-auto px-4">
      <div class="flex justify-between items-center h-16">
        <!-- Logo -->
        <div class="flex items-center space-x-2">
          <div class="w-8 h-8 bg-white rounded-full flex items-center justify-center">
            <Icon name="mdi:rickshaw" class="text-[#009344] text-lg" />
          </div>
          <span class="text-white font-bold text-xl">Becaknesia</span>
        </div>

        <!-- Menu -->
        <div class="hidden md:flex items-center space-x-8">
          <NuxtLink to="/" class="text-white hover:text-[#F4A800] transition-colors">Home</NuxtLink>
          <NuxtLink to="/rute" class="text-white hover:text-[#F4A800] transition-colors">Rute Perjalanan</NuxtLink>
          <NuxtLink to="/souvenir" class="text-white hover:text-[#F4A800] transition-colors">Souvenir</NuxtLink>
          <NuxtLink to="/reservasi" class="text-white hover:text-[#F4A800] transition-colors">Reservasi</NuxtLink>
          <NuxtLink to="/kontak" class="text-white hover:text-[#F4A800] transition-colors">Kontak</NuxtLink>
        </div>

        <!-- Right side -->
        <div class="flex items-center space-x-4">
          <!-- Search -->
          <div class="hidden md:block">
            <input 
              type="text" 
              placeholder="Cari..." 
              class="px-3 py-1 rounded text-sm focus:outline-none focus:ring-2 focus:ring-[#F4A800]"
            />
          </div>
          
          <!-- Language -->
          <select class="bg-transparent text-white text-sm border border-white rounded px-2 py-1">
            <option value="id" class="text-[#1F2937]">ID</option>
            <option value="en" class="text-[#1F2937]">EN</option>
          </select>

          <!-- Contact Button -->
          <button class="bg-[#F4A800] hover:bg-[#e09600] text-white px-6 py-2 rounded font-bold text-sm transition-colors">
            Hubungi Kami
          </button>
        </div>
      </div>
    </div>
  </nav>
</template>
