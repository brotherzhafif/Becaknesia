<template>
  <div>
    <Navbar />
    <main class="min-h-screen bg-[#F7F7F7] py-20 flex items-center justify-center">
      <div class="max-w-md mx-auto px-4">
        <div class="bg-white rounded-xl shadow-md p-8">
          <h1 class="text-2xl font-bold text-[#1F2937] text-center mb-8">Login</h1>
          
          <form @submit.prevent="handleLogin" class="space-y-6">
            <div>
              <label class="block text-sm font-medium text-[#1F2937] mb-2">Email</label>
              <input 
                type="email" 
                required 
                v-model="form.email"
                class="w-full px-3 py-2 border border-[#E5E7EB] rounded focus:outline-none focus:ring-2 focus:ring-[#F4A800]" 
              />
            </div>
            
            <div>
              <label class="block text-sm font-medium text-[#1F2937] mb-2">Password</label>
              <input 
                type="password" 
                required 
                v-model="form.password"
                class="w-full px-3 py-2 border border-[#E5E7EB] rounded focus:outline-none focus:ring-2 focus:ring-[#F4A800]" 
              />
            </div>
            
            <button 
              type="submit" 
              :disabled="loading"
              class="w-full bg-[#F4A800] hover:bg-[#e09600] disabled:bg-gray-400 text-white py-3 rounded font-bold transition-colors"
            >
              {{ loading ? 'Loading...' : 'Login' }}
            </button>
          </form>

          <div v-if="error" class="mt-4 p-3 bg-red-100 border border-red-400 text-red-700 rounded">
            {{ error }}
          </div>
          
          <div class="mt-6 text-center text-sm text-[#6B7280]">
            <p>Belum punya akun? <NuxtLink to="/register" class="text-[#009344] hover:underline">Daftar di sini</NuxtLink></p>
          </div>
        </div>
      </div>
    </main>
    <Footer />
  </div>
</template>

<script setup>
const API_BASE = 'http://70.153.72.39:8011'

const form = ref({
  email: '',
  password: ''
})

const loading = ref(false)
const error = ref('')

const handleLogin = async () => {
  loading.value = true
  error.value = ''
  
  try {
    const response = await $fetch(`${API_BASE}/auth/login`, {
      method: 'POST',
      body: form.value
    })

    if (response.status === 'success') {
      // Store token
      if (process.client) {
        localStorage.setItem('token', response.data.token)
        localStorage.setItem('user', JSON.stringify(response.data.user))
      }
      
      // Redirect based on role
      const user = response.data.user
      if (user.role === 'admin') {
        navigateTo('/admin/dashboard')
      } else if (user.role === 'driver') {
        navigateTo('/driver/dashboard')
      } else {
        navigateTo('/')
      }
    }
  } catch (err) {
    error.value = err.data?.message || 'Login failed. Please try again.'
  } finally {
    loading.value = false
  }
}
</script>
