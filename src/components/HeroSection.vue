<template>
  <div class="relative bg-slate-900 pt-24 pb-16 overflow-hidden">
    <!-- Background Pattern -->
    <div class="absolute inset-0 opacity-10">
      <div class="absolute inset-0"
        style="background-image: url('data:image/svg+xml,%3Csvg%20width%3D%2760%27%20height%3D%2760%27%20viewBox%3D%270%200%2060%2060%27%20xmlns%3D%27http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%27%3E%3Cg%20fill%3D%27none%27%20fill-rule%3D%27evenodd%27%3E%3Cg%20fill%3D%27%23FCD34D%27%20fill-opacity%3D%270.4%27%3E%3Cpath%20d%3D%27M36%2034v-4h-2v4h-4v2h4v4h2v-4h4v-2h-4zm0-30V0h-2v4h-4v2h4v4h2V6h4V4h-4zM6%2034v-4H4v4H0v2h4v4h2v-4h4v-2H6zM6%204V0H4v4H0v2h4v4h2V6h4V4H6z%27%2F%3E%3C%2Fg%3E%3C%2Fg%3E%3C%2Fsvg%3E');">
      </div>
    </div>

    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative">
      <!-- Hero Content -->
      <div class="text-center" v-motion :initial="{ opacity: 0, y: 100 }" :enter="{ opacity: 1, y: 0 }" :duration="800">
        <h1 class="text-4xl md:text-6xl font-bold text-white mb-6 leading-tight">
          <span class="block">Transforming Your</span>
          <span class="text-yellow-400">Investment Future</span>
        </h1>
        <p class="text-xl text-gray-300 mb-8 max-w-3xl mx-auto">
          Expert solutions in Petroleum Trading, Import/Export, and Forex Markets.
          Your gateway to global investment opportunities.
        </p>
        <div class="flex justify-center gap-6">
          <button
            class="group relative px-8 py-3 bg-yellow-400 hover:bg-yellow-500 text-slate-900 rounded-lg font-bold transition-all duration-300 transform hover:scale-105">
            Get Started
            <span
              class="absolute w-full h-full border-2 border-yellow-400 rounded-lg -left-1 -top-1 group-hover:left-0 group-hover:top-0 transition-all duration-300"></span>
          </button>
          <button
            class="px-8 py-3 border-2 border-yellow-400 text-yellow-400 hover:bg-yellow-400 hover:text-slate-900 rounded-lg font-bold transition-all duration-300 transform hover:scale-105">
            Learn More
          </button>
        </div>
      </div>

    <div class="mt-20">
  <div class="relative">
    <div class="overflow-hidden">
      <div
        class="flex transition-transform duration-500 ease-in-out"
        :style="{ transform: `translateX(-${currentPage * 100}%)` }"
      >
        <!-- Each PAGE (group of 3 cards) -->
        <div
          v-for="(page, pIdx) in pages"
          :key="pIdx"
          class="flex gap-6 px-4 py-4 flex-shrink-0 w-full justify-center"
          style="flex: 0 0 100%;"
        >
          <!-- Each CARD -->
          <div
            v-for="(highlight, idx) in page"
            :key="idx"
            class="w-full md:w-1/3"
          >
            <HeroCards :item="highlight" />
          </div>
        </div>
      </div>
    </div>

    <!-- Controls -->
    <button
      class="absolute left-0 top-1/2 -translate-y-1/2 p-2 rounded-full bg-yellow-400 text-slate-900  text-2xl font-bold  hover:bg-slate-500"
      @click="prev"
      aria-label="Previous"
    >
      ‹
    </button>
    <button
      class="absolute right-0 top-1/2 -translate-y-1/2 p-2 rounded-full bg-yellow-400 text-slate-900 hover:bg-slate-500 text-2xl font-bold"
      @click="next"
      aria-label="Next"
    >
      ›
    </button>

    <!-- Dots -->
    <div class="flex justify-center gap-2 mt-4">
      <button
        v-for="n in pages.length"
        :key="n"
        @click="goTo(n - 1)"
        :class="['w-3 h-3 rounded-full', currentPage === (n - 1) ? 'bg-yellow-400' : 'bg-slate-600']"
        aria-label="Go to slide"
      />
    </div>
  </div>
</div>

    </div>

    <!-- Animated Shapes -->
    <div class="absolute -top-20 -right-20 w-64 h-64 bulb bg-yellow-400/20 rounded-full animate-blob"></div>
    <div
      class="absolute -bottom-20 -left-20 w-64 h-64 bulb bg-yellow-400/20 rounded-full animate-blob animation-delay-2000">
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onBeforeUnmount } from 'vue'
import { useMotion } from '@vueuse/motion'
import HeroCards from '../components/HeroCards.vue'
useMotion()

// 9 cards as requested
const highlights = [
  { value: '$50M+', title: 'Trading Volume', description: 'Monthly trading volume across all markets' },
  { value: '15+', title: 'Years Experience', description: 'Professional expertise in global markets' },
  { value: '1000+', title: 'Satisfied Clients', description: 'Trusted by businesses worldwide' },
  { value: '250+', title: 'Partners', description: 'Global strategic partners' },
  { value: '120+', title: 'Markets', description: 'Active markets worldwide' },
  { value: '98%', title: 'Satisfaction', description: 'Client satisfaction rate' },
  { value: '75', title: 'Countries', description: 'Operating in many countries' },
  { value: '500+', title: 'Projects', description: 'Completed projects' },
  { value: '24/7', title: 'Support', description: 'Around the clock support' }
]

const currentPage = ref(0)
const slidesPerView = ref(3)
const track = ref(null)
let autoplayTimer = null

const updateSlidesPerView = () => {
  slidesPerView.value = window.innerWidth >= 768 ? 3 : 1
  // clamp currentPage after slidesPerView change
  currentPage.value = Math.min(currentPage.value, Math.max(0, pages.value.length - 1))
}

// create pages (chunks) of slidesPerView
const pages = computed(() => {
  const chunks = []
  for (let i = 0; i < highlights.length; i += slidesPerView.value) {
    chunks.push(highlights.slice(i, i + slidesPerView.value))
  }
  return chunks
})

function next() {
  const maxPage = Math.max(0, pages.value.length - 1)
  currentPage.value = currentPage.value >= maxPage ? 0 : currentPage.value + 1
  resetAutoplay()
}
function prev() {
  const maxPage = Math.max(0, pages.value.length - 1)
  currentPage.value = currentPage.value <= 0 ? maxPage : currentPage.value - 1
  resetAutoplay()
}
function goTo(i) {
  const maxPage = Math.max(0, pages.value.length - 1)
  currentPage.value = Math.min(Math.max(0, i), maxPage)
  resetAutoplay()
}

function startAutoplay() {
  stopAutoplay()
  autoplayTimer = setInterval(() => next(), 4000)
}
function stopAutoplay() {
  if (autoplayTimer) {
    clearInterval(autoplayTimer)
    autoplayTimer = null
  }
}
function resetAutoplay() {
  stopAutoplay()
  startAutoplay()
}

onMounted(() => {
  updateSlidesPerView()
  window.addEventListener('resize', updateSlidesPerView)
  startAutoplay()
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', updateSlidesPerView)
  stopAutoplay()
})
</script>

<style scoped>
@keyframes blob {
  0% {
    transform: translate(0px, 0px) scale(1);
  }

  33% {
    transform: translate(30px, -30px) scale(1.1);
  }

  66% {
    transform: translate(-20px, 20px) scale(0.9);
  }

  100% {
    transform: translate(0px, 0px) scale(1);
  }
}

.animate-blob {
  animation: blob 7s infinite;
}

.animation-delay-2000 {
  animation-delay: 2s;
}

/* Bulb styling */
.bulb {
  filter: blur(40px);
  mix-blend-mode: screen;
  opacity: 0.9;
  transform: translateZ(0);
  transition: opacity .3s ease;
}

.bulb:hover {
  opacity: 1;
}

/* carousel button sizes */
button[aria-label="Previous"],
button[aria-label="Next"] {
  width: 38px;
  height: 38px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.animate-number {
  animation: fadeInUp 1s ease-out forwards;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* ensure each page takes viewport width */
</style>