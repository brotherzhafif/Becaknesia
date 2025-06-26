<template>
  <div>
    <Navbar />
    <main class="min-h-screen bg-[#F7F7F7] py-20">
      <div class="max-w-2xl mx-auto px-4">
        <h1 class="text-3xl font-bold text-[#1F2937] text-center mb-12">Form Reservasi</h1>
        
        <form @submit.prevent="submitReservation" class="bg-white rounded-xl shadow-md p-8">
          <div class="space-y-6">
            <!-- Personal Info -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <div>
                <label class="block text-sm font-medium text-[#1F2937] mb-2">Nama Lengkap</label>
                <input 
                  type="text" 
                  required 
                  v-model="form.name"
                  class="w-full px-3 py-2 border border-[#E5E7EB] rounded focus:outline-none focus:ring-2 focus:ring-[#F4A800]" 
                />
              </div>
              <div>
                <label class="block text-sm font-medium text-[#1F2937] mb-2">No. WhatsApp</label>
                <input 
                  type="tel" 
                  required 
                  v-model="form.no_hp"
                  class="w-full px-3 py-2 border border-[#E5E7EB] rounded focus:outline-none focus:ring-2 focus:ring-[#F4A800]" 
                />
              </div>
            </div>

            <div>
              <label class="block text-sm font-medium text-[#1F2937] mb-2">Email</label>
              <input 
                type="email" 
                required 
                v-model="form.email"
                class="w-full px-3 py-2 border border-[#E5E7EB] rounded focus:outline-none focus:ring-2 focus:ring-[#F4A800]" 
              />
            </div>

            <!-- Trip Details -->
            <div>
              <label class="block text-sm font-medium text-[#1F2937] mb-2">Pilih Rute Wisata</label>
              <select 
                required 
                v-model="form.tour_id"
                class="w-full px-3 py-2 border border-[#E5E7EB] rounded focus:outline-none focus:ring-2 focus:ring-[#F4A800]"
              >
                <option value="">Pilih rute...</option>
                <option 
                  v-for="tour in tours" 
                  :key="tour._id" 
                  :value="tour._id"
                >
                  {{ tour.route_name }} - Rp {{ formatPrice(tour.prices) }}
                </option>
              </select>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <div>
                <label class="block text-sm font-medium text-[#1F2937] mb-2">Tanggal</label>
                <input 
                  type="date" 
                  required 
                  v-model="form.date"
                  :min="new Date().toISOString().split('T')[0]"
                  class="w-full px-3 py-2 border border-[#E5E7EB] rounded focus:outline-none focus:ring-2 focus:ring-[#F4A800]" 
                />
              </div>
              <div>
                <label class="block text-sm font-medium text-[#1F2937] mb-2">Jam</label>
                <input 
                  type="time" 
                  required 
                  v-model="form.time"
                  class="w-full px-3 py-2 border border-[#E5E7EB] rounded focus:outline-none focus:ring-2 focus:ring-[#F4A800]" 
                />
              </div>
            </div>

            <!-- Passengers -->
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
              <div>
                <label class="block text-sm font-medium text-[#1F2937] mb-2">Dewasa</label>
                <input 
                  type="number" 
                  min="1" 
                  v-model="form.adults"
                  @input="calculateTotal"
                  class="w-full px-3 py-2 border border-[#E5E7EB] rounded focus:outline-none focus:ring-2 focus:ring-[#F4A800]" 
                />
              </div>
              <div>
                <label class="block text-sm font-medium text-[#1F2937] mb-2">Anak (3-12 th)</label>
                <input 
                  type="number" 
                  min="0" 
                  v-model="form.children"
                  @input="calculateTotal"
                  class="w-full px-3 py-2 border border-[#E5E7EB] rounded focus:outline-none focus:ring-2 focus:ring-[#F4A800]" 
                />
              </div>
              <div>
                <label class="block text-sm font-medium text-[#1F2937] mb-2">Bayi (0-2 th)</label>
                <input 
                  type="number" 
                  min="0" 
                  v-model="form.babies"
                  class="w-full px-3 py-2 border border-[#E5E7EB] rounded focus:outline-none focus:ring-2 focus:ring-[#F4A800]" 
                />
              </div>
            </div>

            <!-- Pickup Location -->
            <div>
              <label class="block text-sm font-medium text-[#1F2937] mb-2">Lokasi Penjemputan</label>
              <textarea 
                rows="3" 
                required
                v-model="form.pickup_location"
                placeholder="Masukkan alamat lengkap penjemputan..." 
                class="w-full px-3 py-2 border border-[#E5E7EB] rounded focus:outline-none focus:ring-2 focus:ring-[#F4A800]"
              ></textarea>
            </div>

            <!-- Payment Method -->
            <div>
              <label class="block text-sm font-medium text-[#1F2937] mb-2">Metode Pembayaran</label>
              <div class="space-y-2">
                <label class="flex items-center">
                  <input 
                    type="radio" 
                    name="payment" 
                    value="qris" 
                    v-model="form.payment_method"
                    class="mr-2" 
                  />
                  <span>QRIS (Transfer Digital)</span>
                </label>
                <label class="flex items-center">
                  <input 
                    type="radio" 
                    name="payment" 
                    value="cash" 
                    v-model="form.payment_method"
                    class="mr-2" 
                  />
                  <span>Cash (Bayar di Tempat)</span>
                </label>
              </div>
            </div>

            <!-- Total Price Display -->
            <div v-if="calculatedTotal > 0" class="bg-[#F7F7F7] p-4 rounded-lg">
              <div class="flex justify-between items-center">
                <span class="font-medium">Total Pembayaran:</span>
                <span class="text-xl font-bold text-[#009344]">Rp {{ formatPrice(calculatedTotal) }}</span>
              </div>
            </div>

            <button 
              type="submit" 
              :disabled="loading"
              class="w-full bg-[#F4A800] hover:bg-[#e09600] disabled:bg-gray-400 text-white py-3 rounded font-bold transition-colors"
            >
              {{ loading ? 'Memproses...' : 'Kirim Reservasi' }}
            </button>
          </div>
        </form>
      </div>
    </main>
    <Footer />
  </div>
</template>

<script setup>
const API_BASE = 'http://70.153.72.39:8011'

const form = ref({
  name: '',
  email: '',
  no_hp: '',
  tour_id: '',
  date: '',
  time: '',
  adults: 1,
  children: 0,
  babies: 0,
  pickup_location: '',
  payment_method: 'qris'
})

const tours = ref([])
const loading = ref(false)
const calculatedTotal = ref(0)

// Fetch available tours
const fetchTours = async () => {
  try {
    const response = await $fetch(`${API_BASE}/tour/`)
    tours.value = response.data || []
  } catch (error) {
    console.error('Failed to fetch tours:', error)
  }
}

// Calculate total price
const calculateTotal = () => {
  const selectedTour = tours.value.find(tour => tour._id === form.value.tour_id)
  if (selectedTour) {
    const adultPrice = selectedTour.prices * form.value.adults
    const childPrice = selectedTour.prices * 0.7 * form.value.children // 30% discount for children
    calculatedTotal.value = adultPrice + childPrice
  }
}

// Submit reservation
const submitReservation = async () => {
  loading.value = true
  try {
    // Combine date and time for pickup_time
    const pickup_time = `${form.value.date}T${form.value.time}`
    
    const orderData = {
      tour_id: form.value.tour_id,
      payment_method: form.value.payment_method,
      total: calculatedTotal.value.toString(),
      pickup_location: form.value.pickup_location,
      pickup_time: pickup_time
    }

    // This would require authentication - for demo purposes
    const response = await $fetch(`${API_BASE}/order/`, {
      method: 'POST',
      body: orderData,
      headers: {
        'Authorization': `Bearer ${localStorage.getItem('token') || ''}`
      }
    })

    if (response.status === 'success') {
      // Redirect to payment or success page
      if (form.value.payment_method === 'qris') {
        navigateTo(`/pembayaran?order_id=${response.data._id}`)
      } else {
        navigateTo(`/sukses?order_id=${response.data._id}`)
      }
    }
  } catch (error) {
    console.error('Reservation failed:', error)
    alert('Terjadi kesalahan. Silakan coba lagi.')
  } finally {
    loading.value = false
  }
}

// Format price display
const formatPrice = (price) => {
  return new Intl.NumberFormat('id-ID').format(price)
}

// Fetch tours on mount
onMounted(() => {
  fetchTours()
})

// Watch tour selection to calculate total
watch(() => form.value.tour_id, calculateTotal)
</script>
