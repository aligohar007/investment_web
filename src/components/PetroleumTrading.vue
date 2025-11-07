<template>
  <section class="bg-slate-900 py-20">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- Section Header -->
      <div class="text-center mb-16" 
           v-motion
           :initial="{ opacity: 0, y: 100 }"
           :enter="{ opacity: 1, y: 0 }"
           :duration="800">
        <h2 class="text-3xl md:text-5xl font-bold mb-6">
          <span class="text-white">Global</span>
          <span class="text-yellow-400"> Petroleum Trading</span>
        </h2>
        <p class="text-gray-400 max-w-3xl mx-auto text-lg">
          Leading the energy market with innovative trading solutions and sustainable practices
        </p>
      </div>

      <!-- Features Grid -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-10 mb-16">
        <!-- Left Content -->
        <div class="space-y-8"
             v-motion
             :initial="{ opacity: 0, x: -100 }"
             :enter="{ opacity: 1, x: 0 }"
             :duration="1000">
          <div v-for="(feature, index) in features" :key="index"
               class="bg-slate-800/50 p-6 rounded-xl border border-slate-700 hover:border-yellow-400/50 transition-all duration-300">
            <div class="flex items-start gap-4">
              <div class="bg-yellow-400/10 p-3 rounded-lg">
                <component :is="feature.icon" class="w-6 h-6 text-yellow-400"/>
              </div>
              <div>
                <h3 class="text-white text-xl font-semibold mb-2">{{ feature.title }}</h3>
                <p class="text-gray-400">{{ feature.description }}</p>
              </div>
            </div>
          </div>
        </div>

        <!-- Right Image -->
        <div class="relative rounded-2xl overflow-hidden group"
             v-motion
             :initial="{ opacity: 0, x: 100 }"
             :enter="{ opacity: 1, x: 0 }"
             :duration="1000">
          <img 
            src="../assets/images/deniz-demirci-lOyyTH_0Zic-unsplash.jpg" 
            alt="Petroleum Trading Operations"
            class="w-full h-full object-cover transform group-hover:scale-105 transition-transform duration-700"
          />
          <div class="absolute inset-0 bg-gradient-to-t from-slate-900/80 to-transparent">
            <div class="absolute bottom-6 left-6">
              <div class="flex items-center gap-4 text-white">
                <span class="text-4xl font-bold">25+</span>
                <span class="text-sm">Years of Trading<br/>Excellence</span>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Trading Stats -->
      <div class="grid grid-cols-2 md:grid-cols-4 gap-6 bg-slate-800/30 rounded-xl p-8 backdrop-blur-sm border border-slate-700">
        <div v-for="stat in tradingStats" :key="stat.value" 
             class="text-center"
             v-motion
             :initial="{ opacity: 0, y: 20 }"
             :enter="{ opacity: 1, y: 0 }"
             :delay="200">
          <div class="text-yellow-400 text-3xl font-bold mb-2">{{ stat.value }}</div>
          <div class="text-gray-400 text-sm">{{ stat.label }}</div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
  import { useMotion } from '@vueuse/motion'
  import { BarChart3 , Globe2 } from 'lucide-vue-next'
  useMotion()


const features = [
  {
    icon: BarChart3,
    title: 'Market Analysis',
    description: 'Advanced analytics and real-time market insights for informed trading decisions'
  },
  {
    icon: Globe2,
    title: 'Global Network',
    description: 'Extensive network of suppliers and buyers across major petroleum markets'
  },
]

const tradingStats = [
  { value: '500K+', label: 'Barrels Traded Daily' },
  { value: '45+', label: 'Global Partners' },
  { value: '99.9%', label: 'Delivery Success' },
  { value: '24/7', label: 'Market Monitoring' }
]
</script>

<style scoped>
.backdrop-blur-sm {
  backdrop-filter: blur(8px);
}

/* Optional: Add smooth reveal animations */
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
</style>