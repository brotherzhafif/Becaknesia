<template>
  <section class="bg-[#009344] py-20">
    <div class="max-w-6xl mx-auto px-4 text-center">
      <h1 class="text-5xl font-bold text-white mb-6">
        Naik Becak, Jelajah Budaya dan Wisata Indonesia
      </h1>
      <p class="text-lg text-white mb-8 max-w-3xl mx-auto">
        Dari gang kecil sampai candi megah, rasakan pengalaman wisata otentik dengan becak tradisional. 
        Nikmati perjalanan yang ramah lingkungan sambil mendukung ekonomi lokal.
      </p>
      <div class="flex flex-col sm:flex-row gap-4 justify-center">
        <NuxtLink 
          to="/reservasi" 
          class="bg-[#F4A800] hover:bg-[#e09600] text-white px-8 py-3 rounded font-bold transition-colors"
        >
          Reservasi Sekarang
        </NuxtLink>
        <NuxtLink 
          to="/rute" 
          class="border-2 border-[#F4A800] text-[#F4A800] hover:bg-[#F4A800] hover:text-white px-8 py-3 rounded font-bold transition-colors"
        >
          Rekomendasi Wisata
        </NuxtLink>
      </div>
    </div>
  </section>
</template>
