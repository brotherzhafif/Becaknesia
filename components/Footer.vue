<template>
  <footer class="bg-[#009344] text-white py-12">
    <div class="max-w-6xl mx-auto px-4">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
        <!-- Company Info -->
        <div>
          <div class="flex items-center space-x-2 mb-4">
            <div class="w-8 h-8 bg-white rounded-full flex items-center justify-center">
              <Icon name="mdi:rickshaw" class="text-[#009344] text-lg" />
            </div>
            <span class="font-bold text-xl">Becaknesia</span>
          </div>
          <p class="text-sm leading-relaxed opacity-90">
            Platform wisata becak yang menghubungkan wisatawan dengan pengalaman autentik 
            budaya Indonesia sambil memberdayakan masyarakat lokal.
          </p>
        </div>

        <!-- Navigation Links -->
        <div>
          <h4 class="font-bold mb-4">Menu</h4>
          <ul class="space-y-2 text-sm">
            <li><NuxtLink to="/rute" class="hover:text-[#F4A800] transition-colors">Rute</NuxtLink></li>
            <li><NuxtLink to="/souvenir" class="hover:text-[#F4A800] transition-colors">Souvenir</NuxtLink></li>
            <li><NuxtLink to="/reservasi" class="hover:text-[#F4A800] transition-colors">Reservasi</NuxtLink></li>
            <li><NuxtLink to="/kontak" class="hover:text-[#F4A800] transition-colors">Kontak</NuxtLink></li>
            <li><NuxtLink to="/login" class="hover:text-[#F4A800] transition-colors">Login</NuxtLink></li>
          </ul>
        </div>

        <!-- Contact Info -->
        <div>
          <h4 class="font-bold mb-4">Kontak</h4>
          <div class="space-y-3 text-sm">
            <div class="flex items-start space-x-2">
              <Icon name="mdi:map-marker" class="text-[#F4A800] mt-1" />
              <span>Jl. Malioboro No. 123, Yogyakarta 55271</span>
            </div>
            <div class="flex items-center space-x-2">
              <Icon name="mdi:email" class="text-[#F4A800]" />
              <span>info@becaknesia.com</span>
            </div>
            <div class="flex items-center space-x-2">
              <Icon name="mdi:whatsapp" class="text-[#F4A800]" />
              <span>+62 812-3456-7890</span>
            </div>
          </div>
        </div>
      </div>

      <!-- Bottom bar -->
      <div class="border-t border-white/20 mt-8 pt-8 flex flex-col md:flex-row justify-between items-center">
        <p class="text-sm opacity-75">© 2024 Becaknesia. All rights reserved.</p>
        <div class="flex space-x-4 mt-4 md:mt-0">
          <Icon name="mdi:instagram" class="text-xl hover:text-[#F4A800] cursor-pointer transition-colors" />
          <Icon name="mdi:facebook" class="text-xl hover:text-[#F4A800] cursor-pointer transition-colors" />
          <Icon name="mdi:youtube" class="text-xl hover:text-[#F4A800] cursor-pointer transition-colors" />
          <Icon name="simple-icons:tiktok" class="text-xl hover:text-[#F4A800] cursor-pointer transition-colors" />
        </div>
      </div>
    </div>
  </footer>
</template>
