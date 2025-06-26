<template>
  <div>
    <Navbar />
    <main class="min-h-screen bg-[#F7F7F7] py-20">
      <div class="max-w-4xl mx-auto px-4">
        <h1 class="text-3xl font-bold text-[#1F2937] text-center mb-12">Hubungi Kami</h1>
        
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-12">
          <!-- Contact Info -->
          <div class="bg-white rounded-xl shadow-md p-8">
            <h2 class="text-2xl font-bold text-[#1F2937] mb-6">Informasi Kontak</h2>
            <div class="space-y-6">
              <div class="flex items-start space-x-4">
                <Icon name="mdi:map-marker" class="text-[#F4A800] text-2xl mt-1" />
                <div>
                  <h3 class="font-semibold text-[#1F2937]">Alamat</h3>
                  <p class="text-[#6B7280]">Jl. Malioboro No. 123<br />Yogyakarta 55271<br />Indonesia</p>
                </div>
              </div>
              
              <div class="flex items-start space-x-4">
                <Icon name="mdi:email" class="text-[#F4A800] text-2xl mt-1" />
                <div>
                  <h3 class="font-semibold text-[#1F2937]">Email</h3>
                  <p class="text-[#6B7280]">info@becaknesia.com</p>
                </div>
              </div>
              
              <div class="flex items-start space-x-4">
                <Icon name="mdi:whatsapp" class="text-[#F4A800] text-2xl mt-1" />
                <div>
                  <h3 class="font-semibold text-[#1F2937]">WhatsApp</h3>
                  <p class="text-[#6B7280]">+62 812-3456-7890</p>
                </div>
              </div>
            </div>
          </div>

          <!-- Google Maps Placeholder -->
          <div class="bg-white rounded-xl shadow-md p-8">
            <h2 class="text-2xl font-bold text-[#1F2937] mb-6">Lokasi Kami</h2>
            <div class="h-64 bg-[#F7F7F7] rounded-lg flex items-center justify-center">
              <div class="text-center text-[#6B7280]">
                <Icon name="mdi:map" class="text-6xl mb-2" />
                <p>Google Maps akan ditampilkan di sini</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </main>
    <Footer />
  </div>
</template>
