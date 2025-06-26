<template>
  <div>
    <Navbar />
    <div class="min-h-screen bg-[#F7F7F7] py-20">
      <div class="max-w-4xl mx-auto px-4">
        <h1 class="text-4xl font-bold text-[#1F2937] text-center mb-4">Reservasi Wisata</h1>
        <p class="text-[#6B7280] text-center mb-12">
          Isi formulir di bawah untuk melakukan reservasi paket wisata becak. Tim kami akan menghubungi Anda segera.
        </p>

        <div class="bg-white rounded-xl shadow-lg p-8">
          <form @submit.prevent="submitReservation" class="space-y-6">
            <!-- Personal Information -->
            <div class="border-b border-[#E5E7EB] pb-6">
              <h2 class="text-xl font-bold text-[#1F2937] mb-4">Informasi Pribadi</h2>
              <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div>
                  <label class="block text-sm font-medium text-[#374151] mb-2">Nama Lengkap *</label>
                  <input 
                    v-model="form.name"
                    type="text" 
                    required
                    class="w-full px-4 py-2 border border-[#E5E7EB] rounded-lg focus:outline-none focus:ring-2 focus:ring-[#F4A800]"
                    placeholder="Masukkan nama lengkap"
                  />
                </div>
                <div>
                  <label class="block text-sm font-medium text-[#374151] mb-2">Email *</label>
                  <input 
                    v-model="form.email"
                    type="email" 
                    required
                    class="w-full px-4 py-2 border border-[#E5E7EB] rounded-lg focus:outline-none focus:ring-2 focus:ring-[#F4A800]"
                    placeholder="nama@email.com"
                  />
                </div>
                <div>
                  <label class="block text-sm font-medium text-[#374151] mb-2">No. Telepon *</label>
                  <input 
                    v-model="form.phone"
                    type="tel" 
                    required
                    class="w-full px-4 py-2 border border-[#E5E7EB] rounded-lg focus:outline-none focus:ring-2 focus:ring-[#F4A800]"
                    placeholder="08xxx"
                  />
                </div>
                <div>
                  <label class="block text-sm font-medium text-[#374151] mb-2">Jumlah Peserta *</label>
                  <select 
                    v-model="form.participants"
                    required
                    class="w-full px-4 py-2 border border-[#E5E7EB] rounded-lg focus:outline-none focus:ring-2 focus:ring-[#F4A800]"
                  >
                    <option value="">Pilih jumlah</option>
                    <option value="1">1 Orang</option>
                    <option value="2">2 Orang</option>
                    <option value="3">3 Orang</option>
                    <option value="4">4 Orang</option>
                    <option value="5+">5+ Orang</option>
                  </select>
                </div>
              </div>
            </div>

            <!-- Tour Selection -->
            <div class="border-b border-[#E5E7EB] pb-6">
              <h2 class="text-xl font-bold text-[#1F2937] mb-4">Pilih Paket Wisata</h2>
              <div class="space-y-4">
                <div 
                  v-for="tour in tours"
                  :key="tour.id"
                  :class="[
                    'border-2 rounded-lg p-4 cursor-pointer transition-colors',
                    form.selectedTour === tour.id 
                      ? 'border-[#F4A800] bg-[#FEF3E2]' 
                      : 'border-[#E5E7EB] hover:border-[#F4A800]'
                  ]"
                  @click="form.selectedTour = tour.id"
                >
                  <div class="flex items-center space-x-3">
                    <input 
                      type="radio" 
                      :value="tour.id"
                      v-model="form.selectedTour"
                      class="text-[#F4A800] focus:ring-[#F4A800]"
                    />
                    <div class="flex-1">
                      <h3 class="font-bold text-[#1F2937]">{{ tour.name }}</h3>
                      <p class="text-sm text-[#6B7280] mb-2">{{ tour.description }}</p>
                      <div class="flex justify-between items-center">
                        <span class="text-sm text-[#6B7280]">{{ tour.duration }}</span>
                        <span class="font-bold text-[#009344]">{{ tour.price }}</span>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>

            <!-- Schedule -->
            <div class="border-b border-[#E5E7EB] pb-6">
              <h2 class="text-xl font-bold text-[#1F2937] mb-4">Jadwal Keberangkatan</h2>
              <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div>
                  <label class="block text-sm font-medium text-[#374151] mb-2">Tanggal *</label>
                  <input 
                    v-model="form.date"
                    type="date" 
                    required
                    :min="minDate"
                    class="w-full px-4 py-2 border border-[#E5E7EB] rounded-lg focus:outline-none focus:ring-2 focus:ring-[#F4A800]"
                  />
                </div>
                <div>
                  <label class="block text-sm font-medium text-[#374151] mb-2">Waktu *</label>
                  <select 
                    v-model="form.time"
                    required
                    class="w-full px-4 py-2 border border-[#E5E7EB] rounded-lg focus:outline-none focus:ring-2 focus:ring-[#F4A800]"
                  >
                    <option value="">Pilih waktu</option>
                    <option value="08:00">08:00 WIB</option>
                    <option value="10:00">10:00 WIB</option>
                    <option value="13:00">13:00 WIB</option>
                    <option value="15:00">15:00 WIB</option>
                  </select>
                </div>
              </div>
            </div>

            <!-- Pickup Location -->
            <div class="border-b border-[#E5E7EB] pb-6">
              <h2 class="text-xl font-bold text-[#1F2937] mb-4">Lokasi Penjemputan</h2>
              <textarea 
                v-model="form.pickupLocation"
                required
                rows="3"
                class="w-full px-4 py-2 border border-[#E5E7EB] rounded-lg focus:outline-none focus:ring-2 focus:ring-[#F4A800]"
                placeholder="Masukkan alamat lengkap untuk penjemputan"
              ></textarea>
            </div>

            <!-- Payment Method -->
            <div class="border-b border-[#E5E7EB] pb-6">
              <h2 class="text-xl font-bold text-[#1F2937] mb-4">Metode Pembayaran</h2>
              <div class="space-y-3">
                <label class="flex items-center space-x-3 cursor-pointer">
                  <input 
                    type="radio" 
                    value="cash"
                    v-model="form.paymentMethod"
                    class="text-[#F4A800] focus:ring-[#F4A800]"
                  />
                  <span>Cash (Bayar di tempat)</span>
                </label>
                <label class="flex items-center space-x-3 cursor-pointer">
                  <input 
                    type="radio" 
                    value="qris"
                    v-model="form.paymentMethod"
                    class="text-[#F4A800] focus:ring-[#F4A800]"
                  />
                  <span>QRIS</span>
                </label>
              </div>
            </div>

            <!-- Special Requests -->
            <div>
              <h2 class="text-xl font-bold text-[#1F2937] mb-4">Permintaan Khusus</h2>
              <textarea 
                v-model="form.specialRequests"
                rows="3"
                class="w-full px-4 py-2 border border-[#E5E7EB] rounded-lg focus:outline-none focus:ring-2 focus:ring-[#F4A800]"
                placeholder="Ada permintaan khusus? Tulis di sini (opsional)"
              ></textarea>
            </div>

            <!-- Submit Button -->
            <div class="pt-6">
              <button 
                type="submit"
                :disabled="isSubmitting"
                class="w-full bg-[#F4A800] hover:bg-[#e09600] text-white py-3 px-6 rounded-lg font-bold transition-colors disabled:opacity-50"
              >
                {{ isSubmitting ? 'Memproses...' : 'Kirim Reservasi' }}
              </button>
              <p class="text-sm text-[#6B7280] text-center mt-4">
                * Tim kami akan menghubungi Anda dalam 1x24 jam untuk konfirmasi
              </p>
            </div>
          </form>
        </div>
      </div>
    </div>
    <Footer />
  </div>
</template>

<script setup>
useHead({
  title: 'Reservasi Wisata - Becaknesia',
  meta: [
    { name: 'description', content: 'Lakukan reservasi paket wisata becak dengan mudah. Pilih paket, tentukan jadwal, dan nikmati pengalaman wisata yang tak terlupakan.' }
  ]
})

const isSubmitting = ref(false)

const form = ref({
  name: '',
  email: '',
  phone: '',
  participants: '',
  selectedTour: '',
  date: '',
  time: '',
  pickupLocation: '',
  paymentMethod: 'cash',
  specialRequests: ''
})

const tours = ref([
  {
    id: 1,
    name: "Wisata Kraton & Taman Sari",
    description: "Jelajahi kemegahan Kraton Yogyakarta dan keindahan Taman Sari",
    duration: "3-4 jam",
    price: "Rp 75.000/orang"
  },
  {
    id: 2,
    name: "Malioboro & Sosrowijayan",
    description: "Nikmati suasana khas Malioboro dan gang-gang bersejarah",
    duration: "2-3 jam", 
    price: "Rp 50.000/orang"
  },
  {
    id: 3,
    name: "Kampung Batik & Pasar Tradisional",
    description: "Kunjungi sentra batik dan rasakan kehidupan pasar tradisional",
    duration: "3-4 jam",
    price: "Rp 65.000/orang"
  }
])

const minDate = computed(() => {
  const tomorrow = new Date()
  tomorrow.setDate(tomorrow.getDate() + 1)
  return tomorrow.toISOString().split('T')[0]
})

const submitReservation = async () => {
  isSubmitting.value = true
  
  try {
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 2000))
    
    // Reset form
    Object.keys(form.value).forEach(key => {
      if (key === 'paymentMethod') {
        form.value[key] = 'cash'
      } else {
        form.value[key] = ''
      }
    })
    
    alert('Reservasi berhasil dikirim! Tim kami akan menghubungi Anda segera.')
    navigateTo('/sukses')
    
  } catch (error) {
    alert('Terjadi kesalahan. Silakan coba lagi.')
  } finally {
    isSubmitting.value = false
  }
}
</script>
