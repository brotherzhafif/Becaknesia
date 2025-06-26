<template>
  <div>
    <Navbar />
    <main class="min-h-screen bg-[#F7F7F7] flex items-center justify-center py-20 px-4">
      <div class="max-w-md w-full bg-white rounded-xl shadow-lg p-8">
        <!-- Logo -->
        <div class="text-center mb-8">
          <div class="flex items-center justify-center space-x-2 mb-4">
            <div class="w-10 h-10 bg-[#009344] rounded-full flex items-center justify-center">
              <Icon name="mdi:rickshaw" class="text-white text-xl" />
            </div>
            <span class="text-2xl font-bold text-[#009344]">Becaknesia</span>
          </div>
          <h1 class="text-2xl font-bold text-[#1F2937]">Login Admin/Driver</h1>
          <p class="text-[#6B7280] mt-2">Masuk ke dashboard untuk mengelola sistem</p>
        </div>

        <!-- Login Form -->
        <form @submit.prevent="handleLogin" class="space-y-6">
          <div>
            <label class="block text-sm font-medium text-[#374151] mb-2">Email</label>
            <input 
              v-model="loginForm.email"
              type="email" 
              required
              class="w-full px-4 py-3 border border-[#E5E7EB] rounded-lg focus:outline-none focus:ring-2 focus:ring-[#F4A800]"
              placeholder="admin@becaknesia.com"
            />
          </div>

          <div>
            <label class="block text-sm font-medium text-[#374151] mb-2">Password</label>
            <div class="relative">
              <input 
                v-model="loginForm.password"
                :type="showPassword ? 'text' : 'password'"
                required
                class="w-full px-4 py-3 border border-[#E5E7EB] rounded-lg focus:outline-none focus:ring-2 focus:ring-[#F4A800] pr-12"
                placeholder="Masukkan password"
              />
              <button 
                type="button"
                @click="showPassword = !showPassword"
                class="absolute right-3 top-1/2 transform -translate-y-1/2 text-[#6B7280] hover:text-[#374151]"
              >
                <Icon :name="showPassword ? 'mdi:eye-off' : 'mdi:eye'" class="text-xl" />
              </button>
            </div>
          </div>

          <div>
            <label class="block text-sm font-medium text-[#374151] mb-2">Role</label>
            <select 
              v-model="loginForm.role"
              required
              class="w-full px-4 py-3 border border-[#E5E7EB] rounded-lg focus:outline-none focus:ring-2 focus:ring-[#F4A800]"
            >
              <option value="">Pilih role</option>
              <option value="admin">Admin</option>
              <option value="driver">Driver</option>
            </select>
          </div>

          <div class="flex items-center justify-between">
            <label class="flex items-center">
              <input 
                v-model="loginForm.rememberMe"
                type="checkbox" 
                class="text-[#F4A800] focus:ring-[#F4A800] rounded"
              />
              <span class="ml-2 text-sm text-[#6B7280]">Ingat saya</span>
            </label>
            <a href="#" class="text-sm text-[#F4A800] hover:text-[#e09600]">Lupa password?</a>
          </div>

          <button 
            type="submit"
            :disabled="isLoggingIn"
            class="w-full bg-[#F4A800] hover:bg-[#e09600] text-white py-3 px-6 rounded-lg font-bold transition-colors disabled:opacity-50"
          >
            {{ isLoggingIn ? 'Masuk...' : 'Login' }}
          </button>
        </form>

        <!-- Demo Accounts -->
        <div class="mt-8 p-4 bg-[#F7F7F7] rounded-lg">
          <h3 class="font-bold text-sm text-[#374151] mb-2">Demo Accounts:</h3>
          <div class="space-y-2 text-xs text-[#6B7280]">
            <div>
              <strong>Admin:</strong> admin@becaknesia.com / admin123
            </div>
            <div>
              <strong>Driver:</strong> driver@becaknesia.com / driver123
            </div>
          </div>
        </div>

        <!-- Back to Home -->
        <div class="mt-6 text-center">
          <NuxtLink 
            to="/"
            class="text-sm text-[#6B7280] hover:text-[#F4A800] flex items-center justify-center space-x-1"
          >
            <Icon name="mdi:arrow-left" />
            <span>Kembali ke Beranda</span>
          </NuxtLink>
        </div>
      </div>
    </main>
    <Footer />
  </div>
</template>

<script setup>
useHead({
  title: 'Login Admin/Driver - Becaknesia',
  meta: [
    { name: 'description', content: 'Login dashboard untuk admin dan driver Becaknesia. Kelola sistem wisata becak dengan mudah.' }
  ]
})

const isLoggingIn = ref(false)
const showPassword = ref(false)

const loginForm = ref({
  email: '',
  password: '',
  role: '',
  rememberMe: false
})

const handleLogin = async () => {
  isLoggingIn.value = true
  
  try {
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 1500))
    
    // Demo validation
    const isValidAdmin = loginForm.value.email === 'admin@becaknesia.com' && 
                        loginForm.value.password === 'admin123' && 
                        loginForm.value.role === 'admin'
    
    const isValidDriver = loginForm.value.email === 'driver@becaknesia.com' && 
                         loginForm.value.password === 'driver123' && 
                         loginForm.value.role === 'driver'
    
    if (isValidAdmin) {
      navigateTo('/admin/dashboard')
    } else if (isValidDriver) {
      navigateTo('/driver/dashboard')
    } else {
      alert('Email, password, atau role tidak valid!')
    }
    
  } catch (error) {
    alert('Terjadi kesalahan. Silakan coba lagi.')
  } finally {
    isLoggingIn.value = false
  }
}
</script>
