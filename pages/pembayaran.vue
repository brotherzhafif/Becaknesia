<template>
  <div>
    <Navbar />
    <main class="min-h-screen bg-[#F7F7F7] py-20">
      <div class="max-w-2xl mx-auto px-4">
        <h1 class="text-3xl font-bold text-[#1F2937] text-center mb-12">Pembayaran</h1>
        
        <div class="bg-white rounded-xl shadow-md p-8">
          <!-- Order Summary -->
          <div class="mb-8 p-6 bg-[#F7F7F7] rounded-lg">
            <h2 class="text-xl font-bold text-[#1F2937] mb-4">Ringkasan Pesanan</h2>
            <div class="space-y-2 text-sm" v-if="orderDetails">
              <div class="flex justify-between">
                <span>Rute:</span>
                <span class="font-medium">{{ orderDetails.tour_id?.route_name || 'Loading...' }}</span>
              </div>
              <div class="flex justify-between">
                <span>Tanggal:</span>
                <span class="font-medium">{{ formatDate(orderDetails.pickup_time) }}</span>
              </div>
              <div class="flex justify-between">
                <span>Lokasi Pickup:</span>
                <span class="font-medium">{{ orderDetails.pickup_location }}</span>
              </div>
              <div class="border-t pt-2 mt-2 flex justify-between font-bold text-lg">
                <span>Total:</span>
                <span class="text-[#009344]">Rp {{ formatPrice(orderDetails.total) }}</span>
              </div>
            </div>
          </div>

          <!-- QRIS Payment -->
          <div class="text-center">
            <h3 class="text-lg font-bold text-[#1F2937] mb-4">Scan QRIS untuk Pembayaran</h3>
            
            <!-- Timer -->
            <div class="mb-6">
              <div class="text-2xl font-bold text-[#F4A800]">{{ formatTime(timeLeft) }}</div>
              <div class="text-sm text-[#6B7280]">Waktu pembayaran tersisa</div>
            </div>

            <!-- QR Code -->
            <div class="flex justify-center mb-6">
              <div class="w-64 h-64 bg-[#F7F7F7] rounded-lg flex items-center justify-center border-2 border-dashed border-[#E5E7EB]">
                <div class="text-center text-[#6B7280]">
                  <Icon name="mdi:qrcode" class="text-8xl mb-2" />
                  <p class="text-sm">QR Code QRIS</p>
                  <p class="text-xs mt-2">Scan dengan aplikasi pembayaran digital</p>
                </div>
              </div>
            </div>

            <!-- Actions -->
            <div class="space-y-4">
              <button 
                @click="refreshQRCode"
                class="w-full bg-[#009344] hover:bg-[#006B34] text-white py-3 rounded font-bold transition-colors"
              >
                Muat Ulang QR Code
              </button>
              <button 
                @click="cancelPayment"
                class="w-full border border-[#E5E7EB] text-[#6B7280] hover:bg-[#F7F7F7] py-3 rounded font-bold transition-colors"
              >
                Batalkan Pembayaran
              </button>
              <button 
                @click="simulatePaymentSuccess"
                class="w-full bg-[#F4A800] hover:bg-[#e09600] text-white py-3 rounded font-bold transition-colors text-sm"
              >
                Simulasi Pembayaran Berhasil (Demo)
              </button>
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
const API_BASE = 'http://70.153.72.39:8011'
const route = useRoute()
const orderId = route.query.order_id

const timeLeft = ref(15 * 60) // 15 minutes in seconds
const orderDetails = ref(null)
const timer = ref(null)

// Format time display
const formatTime = (seconds) => {
  const minutes = Math.floor(seconds / 60)
  const remainingSeconds = seconds % 60
  return `${minutes.toString().padStart(2, '0')}:${remainingSeconds.toString().padStart(2, '0')}`
}

// Format price display
const formatPrice = (price) => {
  return new Intl.NumberFormat('id-ID').format(price)
}

// Format date display
const formatDate = (dateString) => {
  return new Date(dateString).toLocaleDateString('id-ID', {
    day: 'numeric',
    month: 'long',
    year: 'numeric',
    hour: '2-digit',
    minute: '2-digit'
  })
}

// Start countdown timer
const startTimer = () => {
  timer.value = setInterval(() => {
    timeLeft.value--
    if (timeLeft.value <= 0) {
      clearInterval(timer.value)
      // Auto redirect to failed payment or order cancellation
      cancelPayment()
    }
  }, 1000)
}

// Fetch order details
const fetchOrderDetails = async () => {
  if (!orderId) {
    navigateTo('/reservasi')
    return
  }
  
  try {
    const response = await $fetch(`${API_BASE}/order/${orderId}`, {
      headers: {
        'Authorization': `Bearer ${localStorage.getItem('token') || ''}`
      }
    })
    orderDetails.value = response.data
  } catch (error) {
    console.error('Failed to fetch order details:', error)
    navigateTo('/reservasi')
  }
}

// Refresh QR Code
const refreshQRCode = () => {
  // In real implementation, this would generate a new QR code
  console.log('Refreshing QR Code...')
}

// Cancel payment
const cancelPayment = async () => {
  try {
    await $fetch(`${API_BASE}/order/${orderId}`, {
      method: 'PUT',
      body: { order_status: 'canceled' },
      headers: {
        'Authorization': `Bearer ${localStorage.getItem('token') || ''}`
      }
    })
    navigateTo('/reservasi')
  } catch (error) {
    console.error('Failed to cancel payment:', error)
    navigateTo('/reservasi')
  }
}

// Simulate payment success (for demo)
const simulatePaymentSuccess = async () => {
  try {
    await $fetch(`${API_BASE}/order/${orderId}`, {
      method: 'PUT',
      body: { 
        payment_status: 'success',
        order_status: 'accepted' 
      },
      headers: {
        'Authorization': `Bearer ${localStorage.getItem('token') || ''}`
      }
    })
    navigateTo(`/sukses?order_id=${orderId}`)
  } catch (error) {
    console.error('Failed to update payment status:', error)
  }
}

// Cleanup timer on unmount
onUnmounted(() => {
  if (timer.value) {
    clearInterval(timer.value)
  }
})
</script>
