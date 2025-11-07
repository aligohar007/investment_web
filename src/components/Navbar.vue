<template>
  <div class="relative">
    <header class="bg-slate-900 shadow-lg fixed w-full top-0 z-50">
      <div class="max-w-8xl mx-auto px-4 sm:px-6 lg:px-30">
        <div class="flex justify-between h-20">
          <div class="flex items-center">
            <button @click="toggleSidebar"
              class="md:hidden p-2 rounded-md hover:bg-slate-800 focus:outline-none text-white">
              <svg v-if="!isOpen" class="h-6 w-6" viewBox="0 0 24 24">
                <path stroke="currentColor" stroke-width="2" stroke-linecap="round" d="M3 6h18M3 12h18M3 18h18" />
              </svg>
              <svg v-else class="h-6 w-6" viewBox="0 0 24 24">
                <path stroke="currentColor" stroke-width="2" stroke-linecap="round" d="M6 6l12 12M6 18L18 6" />
              </svg>
            </button>

            <router-link to="/" class="flex items-center">
              <!-- <img src="/investment-logo.png" alt="Investment Logo" class="h-12 w-auto ml-3"/> -->
              <span class="text-2xl font-bold text-white ml-2 cursor-pointer">Global Investments</span>
            </router-link>
          </div>

          <!-- Desktop Navigation -->
          <nav class="hidden md:flex items-center space-x-6 cursor-pointer">
            <template v-for="(link, index) in navLinks" :key="index">
              <a v-if="link.isButton" :href="link.path"
                class="px-10 py-3 bg-yellow-400 rounded-lg text-black font-semibold hover:bg-yellow-500 transition">
                {{ link.name }}
              </a>

              <router-link v-else :to="link.path"
                class="text-gray-300 hover:text-yellow-400 transition-colors duration-200 font-medium text-lg">
                {{ link.name }}
              </router-link>
            </template>
          </nav>

        </div>
      </div>
    </header>

    <!-- Mobile Sidebar -->
    <div class="fixed inset-0 z-40 transform ease-in-out duration-300"
      :class="isOpen ? 'translate-x-0' : '-translate-x-full'">
      <div class="absolute inset-0 bg-black bg-opacity-50" @click="closeSidebar"></div>
      <nav class="relative w-72 max-w-sm bg-slate-900 h-full shadow-xl flex flex-col radiusbox">
        <div class="p-4 border-b border-slate-700 flex justify-between items-center ">
          <span class="font-bold text-xl text-white">Investment Menu</span>
          <button @click="closeSidebar" class="p-2 rounded-md hover:bg-slate-800 focus:outline-none text-white">
            <svg class="h-6 w-6" viewBox="0 0 24 24">
              <path stroke="currentColor" stroke-width="2" stroke-linecap="round" d="M6 6l12 12M6 18L18 6" />
            </svg>
          </button>
        </div>
        <div class="flex-1 overflow-y-auto  m-4 rounded-lg">
          <div class="px-2 py-4 space-y-2">
            <template v-for="(link, index) in navLinks" :key="index">
              <a v-if="link.isButton" :href="link.path"
                class="block px-4 py-3 text-center bg-yellow-400 rounded-md text-black font-semibold hover:bg-yellow-500 transition"
                @click="closeSidebar">
                {{ link.name }}
              </a>

              <router-link v-else :to="link.path" @click="closeSidebar"
                class="block px-4 py-3 text-gray-300 hover:bg-slate-800 hover:text-yellow-400 rounded-md transition-colors duration-200">
                {{ link.name }}
              </router-link>
            </template>
          </div>
        </div>

      </nav>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const isOpen = ref(false)

const navLinks = [
  { name: 'Home', path: '/' },
  { name: 'Petroleum Trading', path: '/petroleum' },
  { name: 'Import/Export', path: '/trade' },
  { name: 'Forex Trading', path: '/forex' },
  { name: 'Market Analysis', path: '/analysis' },
  { name: 'Contact Us', path: '/contact' },
  { name: 'Call Now', path: 'tel:+923001234567', isButton: true }
]

const toggleSidebar = () => {
  isOpen.value = !isOpen.value
}

const closeSidebar = () => {
  isOpen.value = false
}
</script>

<style scoped>
  .radiusbox {
        border-top-right-radius: 200px;
    border-bottom-right-radius: 102px;
  }
</style>