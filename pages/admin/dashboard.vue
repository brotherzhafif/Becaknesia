<template>
  <div class="min-h-screen bg-[#F7F7F7]">
    <!-- Admin Header -->
    <header class="bg-[#009344] text-white py-4">
      <div class="max-w-6xl mx-auto px-4 flex justify-between items-center">
        <h1 class="text-xl font-bold">Admin Dashboard</h1>
        <button class="text-sm hover:text-[#F4A800]">Logout</button>
      </div>
    </header>

    <main class="max-w-6xl mx-auto px-4 py-8">
      <!-- Stats Cards -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-8">
        <div class="bg-white rounded-lg shadow-md p-6">
          <div class="flex items-center justify-between">
            <div>
              <p class="text-[#6B7280] text-sm">Total Users</p>
              <p class="text-2xl font-bold text-[#1F2937]">1,234</p>
            </div>
            <Icon name="mdi:account-group" class="text-[#F4A800] text-4xl" />
          </div>
        </div>
        
        <div class="bg-white rounded-lg shadow-md p-6">
          <div class="flex items-center justify-between">
            <div>
              <p class="text-[#6B7280] text-sm">Total Drivers</p>
              <p class="text-2xl font-bold text-[#1F2937]">56</p>
            </div>
            <Icon name="mdi:rickshaw" class="text-[#F4A800] text-4xl" />
          </div>
        </div>
        
        <div class="bg-white rounded-lg shadow-md p-6">
          <div class="flex items-center justify-between">
            <div>
              <p class="text-[#6B7280] text-sm">Total Orders</p>
              <p class="text-2xl font-bold text-[#1F2937]">789</p>
            </div>
            <Icon name="mdi:clipboard-list" class="text-[#F4A800] text-4xl" />
          </div>
        </div>
      </div>

      <!-- Recent Orders -->
      <div class="bg-white rounded-lg shadow-md p-6">
        <h2 class="text-xl font-bold text-[#1F2937] mb-4">Order Terbaru</h2>
        <div class="overflow-x-auto">
          <table class="w-full">
            <thead>
              <tr class="border-b">
                <th class="text-left py-2">ID</th>
                <th class="text-left py-2">Customer</th>
                <th class="text-left py-2">Rute</th>
                <th class="text-left py-2">Status</th>
                <th class="text-left py-2">Aksi</th>
              </tr>
            </thead>
            <tbody>
              <tr class="border-b">
                <td class="py-2">#001</td>
                <td class="py-2">John Doe</td>
                <td class="py-2">Kraton & Taman Sari</td>
                <td class="py-2"><span class="bg-[#F4A800] text-white px-2 py-1 rounded text-xs">Pending</span></td>
                <td class="py-2">
                  <button class="text-[#009344] hover:underline text-sm">View</button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </main>
  </div>
</template>
