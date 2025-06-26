<template>
  <div>
    <Navbar />
    <div class="min-h-screen bg-white py-20">
      <div class="max-w-6xl mx-auto px-4">
        <h1 class="text-4xl font-bold text-[#1F2937] text-center mb-4">Hubungi Kami</h1>
        <p class="text-[#6B7280] text-center mb-12 max-w-2xl mx-auto">
          Ada pertanyaan atau butuh bantuan? Tim kami siap membantu Anda. Hubungi kami melalui berbagai cara di bawah ini.
        </p>

        <div class="grid grid-cols-1 lg:grid-cols-2 gap-12">
          <!-- Contact Information -->
          <div class="space-y-8">
            <h2 class="text-2xl font-bold text-[#1F2937] mb-6">Informasi Kontak</h2>
            
            <!-- Address -->
            <div class="flex items-start space-x-4">
              <div class="w-12 h-12 bg-[#F4A800] rounded-full flex items-center justify-center flex-shrink-0">
                <Icon name="mdi:map-marker" class="text-white text-xl" />
              </div>
              <div>
                <h3 class="font-bold text-[#1F2937] mb-1">Alamat Kantor</h3>
                <p class="text-[#6B7280]">
                  Jl. Malioboro No. 123<br>
                  Sosromenduran, Gedong Tengen<br>
                  Yogyakarta 55271, Indonesia
                </p>
              </div>
            </div>

            <!-- Phone -->
            <div class="flex items-start space-x-4">
              <div class="w-12 h-12 bg-[#F4A800] rounded-full flex items-center justify-center flex-shrink-0">
                <Icon name="mdi:phone" class="text-white text-xl" />
              </div>
              <div>
                <h3 class="font-bold text-[#1F2937] mb-1">Telepon</h3>
                <p class="text-[#6B7280]">+62 274 555 0123</p>
                <p class="text-sm text-[#6B7280]">Senin - Minggu: 08:00 - 20:00 WIB</p>
              </div>
            </div>

            <!-- WhatsApp -->
            <div class="flex items-start space-x-4">
              <div class="w-12 h-12 bg-[#F4A800] rounded-full flex items-center justify-center flex-shrink-0">
                <Icon name="mdi:whatsapp" class="text-white text-xl" />
              </div>
              <div>
                <h3 class="font-bold text-[#1F2937] mb-1">WhatsApp</h3>
                <p class="text-[#6B7280]">+62 812-3456-7890</p>
                <p class="text-sm text-[#6B7280]">Respon cepat 24/7</p>
                <a 
                  href="https://wa.me/6281234567890" 
                  target="_blank"
                  class="inline-block mt-2 bg-[#25D366] text-white px-4 py-2 rounded text-sm hover:bg-[#20b954] transition-colors"
                >
                  Chat WhatsApp
                </a>
              </div>
            </div>

            <!-- Email -->
            <div class="flex items-start space-x-4">
              <div class="w-12 h-12 bg-[#F4A800] rounded-full flex items-center justify-center flex-shrink-0">
                <Icon name="mdi:email" class="text-white text-xl" />
              </div>
              <div>
                <h3 class="font-bold text-[#1F2937] mb-1">Email</h3>
                <p class="text-[#6B7280]">info@becaknesia.com</p>
                <p class="text-sm text-[#6B7280]">Untuk pertanyaan umum</p>
                <br>
                <p class="text-[#6B7280]">reservasi@becaknesia.com</p>
                <p class="text-sm text-[#6B7280]">Untuk reservasi dan booking</p>
              </div>
            </div>

            <!-- Social Media -->
            <div class="flex items-start space-x-4">
              <div class="w-12 h-12 bg-[#F4A800] rounded-full flex items-center justify-center flex-shrink-0">
                <Icon name="mdi:share-variant" class="text-white text-xl" />
              </div>
              <div>
                <h3 class="font-bold text-[#1F2937] mb-1">Media Sosial</h3>
                <div class="flex space-x-4 mt-2">
                  <a href="#" class="text-[#6B7280] hover:text-[#F4A800] transition-colors">
                    <Icon name="mdi:instagram" class="text-2xl" />
                  </a>
                  <a href="#" class="text-[#6B7280] hover:text-[#F4A800] transition-colors">
                    <Icon name="mdi:facebook" class="text-2xl" />
                  </a>
                  <a href="#" class="text-[#6B7280] hover:text-[#F4A800] transition-colors">
                    <Icon name="mdi:youtube" class="text-2xl" />
                  </a>
                  <a href="#" class="text-[#6B7280] hover:text-[#F4A800] transition-colors">
                    <Icon name="simple-icons:tiktok" class="text-2xl" />
                  </a>
                </div>
              </div>
            </div>
          </div>

          <!-- Contact Form -->
          <div class="bg-[#F7F7F7] rounded-xl p-8">
            <h2 class="text-2xl font-bold text-[#1F2937] mb-6">Kirim Pesan</h2>
            <form @submit.prevent="submitMessage" class="space-y-6">
              <div>
                <label class="block text-sm font-medium text-[#374151] mb-2">Nama Lengkap *</label>
                <input 
                  v-model="contactForm.name"
                  type="text" 
                  required
                  class="w-full px-4 py-2 border border-[#E5E7EB] rounded-lg focus:outline-none focus:ring-2 focus:ring-[#F4A800] bg-white"
                  placeholder="Masukkan nama lengkap"
                />
              </div>
              
              <div>
                <label class="block text-sm font-medium text-[#374151] mb-2">Email *</label>
                <input 
                  v-model="contactForm.email"
                  type="email" 
                  required
                  class="w-full px-4 py-2 border border-[#E5E7EB] rounded-lg focus:outline-none focus:ring-2 focus:ring-[#F4A800] bg-white"
                  placeholder="nama@email.com"
                />
              </div>

              <div>
                <label class="block text-sm font-medium text-[#374151] mb-2">Subjek *</label>
                <select 
                  v-model="contactForm.subject"
                  required
                  class="w-full px-4 py-2 border border-[#E5E7EB] rounded-lg focus:outline-none focus:ring-2 focus:ring-[#F4A800] bg-white"
                >
                  <option value="">Pilih subjek</option>
                  <option value="reservasi">Pertanyaan Reservasi</option>
                  <option value="info">Informasi Paket Wisata</option>
                  <option value="keluhan">Keluhan & Saran</option>
                  <option value="kerjasama">Kerjasama & Partnership</option>
                  <option value="lainnya">Lainnya</option>
                </select>
              </div>

              <div>
                <label class="block text-sm font-medium text-[#374151] mb-2">Pesan *</label>
                <textarea 
                  v-model="contactForm.message"
                  required
                  rows="5"
                  class="w-full px-4 py-2 border border-[#E5E7EB] rounded-lg focus:outline-none focus:ring-2 focus:ring-[#F4A800] bg-white"
                  placeholder="Tulis pesan Anda di sini"
                ></textarea>
              </div>

              <button 
                type="submit"
                :disabled="isSubmittingMessage"
                class="w-full bg-[#F4A800] hover:bg-[#e09600] text-white py-3 px-6 rounded-lg font-bold transition-colors disabled:opacity-50"
              >
                {{ isSubmittingMessage ? 'Mengirim...' : 'Kirim Pesan' }}
              </button>
            </form>
          </div>
        </div>

        <!-- Operating Hours -->
        <div class="mt-16 bg-[#009344] rounded-xl p-8 text-white text-center">
          <h2 class="text-2xl font-bold mb-4">Jam Operasional</h2>
          <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
            <div>
              <h3 class="font-bold mb-2">Customer Service</h3>
              <p>Senin - Minggu</p>
              <p>08:00 - 20:00 WIB</p>
            </div>
            <div>
              <h3 class="font-bold mb-2">Wisata Becak</h3>
              <p>Setiap Hari</p>
              <p>08:00 - 17:00 WIB</p>
            </div>
            <div>
              <h3 class="font-bold mb-2">WhatsApp Support</h3>
              <p>24/7</p>
              <p>Respon Cepat</p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <Footer />
  </div>
</template>

<script setup>
useHead({
  title: 'Hubungi Kami - Becaknesia',
  meta: [
    { name: 'description', content: 'Hubungi tim Becaknesia untuk pertanyaan, reservasi, atau bantuan. Kami siap melayani Anda melalui telepon, WhatsApp, email, dan media sosial.' }
  ]
})

const isSubmittingMessage = ref(false)

const contactForm = ref({
  name: '',
  email: '',
  subject: '',
  message: ''
})

const submitMessage = async () => {
  isSubmittingMessage.value = true
  
  try {
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 1500))
    
    // Reset form
    Object.keys(contactForm.value).forEach(key => {
      contactForm.value[key] = ''
    })
    
    alert('Pesan berhasil dikirim! Tim kami akan merespon dalam 1x24 jam.')
    
  } catch (error) {
    alert('Terjadi kesalahan. Silakan coba lagi.')
  } finally {
    isSubmittingMessage.value = false
  }
}
</script>
