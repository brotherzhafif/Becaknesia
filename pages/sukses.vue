<template>
  <div>
    <Navbar />
    <main class="min-h-screen bg-[#F7F7F7] py-20 flex items-center justify-center">
      <div class="max-w-md mx-auto px-4 text-center">
        <div class="bg-white rounded-xl shadow-md p-8">
          <div class="w-20 h-20 bg-[#009344] rounded-full flex items-center justify-center mx-auto mb-6">
            <Icon name="mdi:check" class="text-white text-4xl" />
          </div>
          
          <h1 class="text-2xl font-bold text-[#1F2937] mb-4">Reservasi Berhasil!</h1>
          <p class="text-[#6B7280] mb-6">
            Terima kasih! Reservasi Anda telah berhasil dikonfirmasi. 
            Kami akan menghubungi Anda melalui WhatsApp untuk koordinasi lebih lanjut.
          </p>
          
          <div class="space-y-3">
            <NuxtLink 
              to="/" 
              class="block w-full bg-[#F4A800] hover:bg-[#e09600] text-white py-3 rounded font-bold transition-colors"
            >
              Kembali ke Beranda
            </NuxtLink>
            <NuxtLink 
              to="/order" 
              class="block w-full border border-[#E5E7EB] text-[#6B7280] hover:bg-[#F7F7F7] py-3 rounded font-bold transition-colors"
            >
              Lihat Pesanan Saya
            </NuxtLink>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
// Check if user came from successful payment
const route = useRoute()
const orderId = route.query.order_id

// Optional: Fetch order details to show specific information
onMounted(() => {
  if (orderId) {
    // Could fetch order details here if needed
    console.log('Order completed:', orderId)
  }
})
</script>
