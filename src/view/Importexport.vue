<template>
  <section 
    class="bg-slate-900 py-30 backdrop-blur-sm lg:py-40"
   
  >
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex flex-col md:flex-row gap-12">
        <!-- Left: Import & Export lists -->
        <div class="flex-1 space-y-6">
          <div class="text-center md:text-left" v-motion :initial="{ opacity: 0, x: -50 }" :enter="{ opacity: 1, x: 0 }" :delay="200">
            <h2 class="text-3xl md:text-4xl font-bold text-white leading-tight">
              Import & Export Services
            </h2>
            <p class="text-gray-400 mt-2 max-w-xl">
              End-to-end logistics and trade solutions — powered by market expertise and global partners.
            </p>
          </div>

          <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <!-- Imports -->
            <div v-motion :initial="{ opacity: 0, x: -50 }" :enter="{ opacity: 1, x: 0 }" :delay="400">
              <h4 class="text-yellow-400 font-semibold mb-3">Imports</h4>
              <div class="grid gap-4">
                <TradeCard
                  v-for="(item, i) in imports"
                  :key="'imp-'+i"
                  :item="item"
                  type="Import"
                  @select="onSelect"
                />
              </div>
            </div>

            <!-- Exports -->
            <div v-motion :initial="{ opacity: 0, x: 50 }" :enter="{ opacity: 1, x: 0 }" :delay="600">
              <h4 class="text-yellow-400 font-semibold mb-3">Exports</h4>
              <div class="grid gap-4">
                <TradeCard
                  v-for="(item, i) in exports"
                  :key="'exp-'+i"
                  :item="item"
                  type="Export"
                  @select="onSelect"
                />
              </div>
            </div>
          </div>
        </div>

        <!-- Right: Details panel -->
        <div class="w-full md:w-1/3"
         v-motion 
        :initial="{ opacity: 0, x: 100 }" 
        :enter="{ opacity: 1, x: 0 }" 
        :delay="800">
          <h4 class="text-yellow-400 font-semibold mb-4">Details</h4>
          <TradeDetails :item="selected" />
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
import TradeCard from '../components/TradeCard.vue'
import TradeDetails from '../components/TradeDetails.vue'


const selected = ref(null)

function onSelect(item) {
  selected.value = item
}

const imports = [
  {
    value: '120K bbl',
    title: 'Crude Oil (Brent)',
    description: 'Sourced from trusted producers, blended to specification.',
    origin: 'Middle East',
    destinations: 'Pakistan, India',
    capacity: '120,000 barrels / shipment',
    image: '/src/assets/images/import1.jpg'
  },
  {
    value: '40K t',
    title: 'Refined Petroleum',
    description: 'High-quality refined products for distribution.',
    origin: 'South Korea',
    destinations: 'Regional Hubs',
    capacity: '40,000 tons / consignment',
    image: '/src/assets/images/import1.jpg'
  }
]

const exports = [
  {
    value: '60K bbl',
    title: 'Diesel Bulk',
    description: 'Marine and land distribution grade diesel.',
    origin: 'Pakistan',
    destinations: 'Africa, Middle East',
    capacity: '60,000 barrels / shipment',
    image: '/src/assets/images/export1.jpg'
  },
  {
    value: '20K t',
    title: 'LPG Cylinders',
    description: 'Packaged LPG for retail and industrial buyers.',
    origin: 'Local Terminals',
    destinations: 'Domestic Market',
    capacity: '20,000 tons',
    image: '/src/assets/images/export1.jpg'
  }
]
</script>

<style scoped>
.backdrop-blur-sm { backdrop-filter: blur(8px); }
</style>
