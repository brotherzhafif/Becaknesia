<template>
  <div class="min-h-screen bg-[#F7F7F7] flex items-center justify-center px-4">
    <div class="max-w-md w-full bg-white rounded-xl shadow-lg p-8 text-center">
      <!-- Success Icon -->
      <div class="w-20 h-20 bg-[#10B981] rounded-full flex items-center justify-center mx-auto mb-6">
        <Icon name="mdi:check" class="text-white text-4xl" />
      </div>

      <!-- Success Message -->
      <h1 class="text-2xl font-bold text-[#1F2937] mb-4">Reservasi Berhasil!</h1>
      <p class="text-[#6B7280] mb-8">
        Terima kasih telah memilih Becaknesia. Reservasi Anda telah berhasil dikirim dan tim kami akan menghubungi Anda segera untuk konfirmasi.
      </p>

      <!-- Next Steps -->
      <div class="bg-[#F7F7F7] rounded-lg p-6 mb-8 text-left">
        <h2 class="font-bold text-[#1F2937] mb-4">Langkah Selanjutnya:</h2>
        <ul class="space-y-3 text-sm text-[#6B7280]">
          <li class="flex items-start space-x-2">
            <Icon name="mdi:numeric-1-circle" class="text-[#F4A800] text-lg flex-shrink-0 mt-0.5" />
            <span>Tim kami akan menghubungi Anda dalam 1x24 jam untuk konfirmasi</span>
          </li>
          <li class="flex items-start space-x-2">
            <Icon name="mdi:numeric-2-circle" class="text-[#F4A800] text-lg flex-shrink-0 mt-0.5" />
            <span>Detail jadwal dan lokasi penjemputan akan dikonfirmasi</span>
          </li>
          <li class="flex items-start space-x-2">
            <Icon name="mdi:numeric-3-circle" class="text-[#F4A800] text-lg flex-shrink-0 mt-0.5" />
            <span>Bersiaplah untuk pengalaman wisata yang tak terlupakan!</span>
          </li>
        </ul>
      </div>

      <!-- Contact Info -->
      <div class="border-t border-[#E5E7EB] pt-6 mb-6">
        <p class="text-sm text-[#6B7280] mb-4">
          Ada pertanyaan? Hubungi kami:
        </p>
        <div class="flex justify-center space-x-6">
          <a 
            href="https://wa.me/6281234567890"
            target="_blank"
            class="flex items-center space-x-2 text-[#25D366] hover:text-[#20b954] transition-colors"
          >
            <Icon name="mdi:whatsapp" class="text-xl" />
            <span class="text-sm">WhatsApp</span>
          </a>
          <a 
            href="tel:+6227455550123"
            class="flex items-center space-x-2 text-[#F4A800] hover:text-[#e09600] transition-colors"
          >
            <Icon name="mdi:phone" class="text-xl" />
            <span class="text-sm">Telepon</span>
          </a>
        </div>
      </div>

      <!-- Action Buttons -->
      <div class="space-y-3">
        <NuxtLink 
          to="/"
          class="w-full bg-[#F4A800] hover:bg-[#e09600] text-white py-3 px-6 rounded-lg font-bold transition-colors block text-center"
        >
          Kembali ke Beranda
        </NuxtLink>
        <NuxtLink 
          to="/rute"
          class="w-full border-2 border-[#F4A800] text-[#F4A800] hover:bg-[#F4A800] hover:text-white py-3 px-6 rounded-lg font-bold transition-colors block text-center"
        >
          Lihat Paket Lainnya
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script setup>
useHead({
  title: 'Reservasi Berhasil - Becaknesia',
  meta: [
    { name: 'description', content: 'Reservasi wisata becak Anda berhasil dikirim. Tim Becaknesia akan segera menghubungi Anda untuk konfirmasi.' }
  ]
})
</script>
