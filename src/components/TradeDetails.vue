<template>
  <div v-if="item" class="bg-slate-800/40 p-6 rounded-xl border border-slate-700">
    <div class="flex gap-6">
      <img v-if="item.image" :src="item.image" :alt="item.title" class="w-20 h-28 object-cover rounded-md" />
      <div>
        <div class="text-yellow-400 text-3xl font-bold">{{ item.value }}</div>
        <h3 class="text-white text-2xl font-semibold my-2">{{ item.title }}</h3>
        <p class="text-gray-300 mb-4">{{ item.description }}</p>
        <ul class="text-sm text-gray-400 space-y-2">
          <li><strong class="text-white">Origin:</strong> {{ item.origin || 'Global' }}</li>
          <li><strong class="text-white">Destinations:</strong> {{ item.destinations || 'Multiple' }}</li>
          <li><strong class="text-white">Capacity:</strong> {{ item.capacity || 'Negotiable' }}</li>
        </ul>
      </div>
    </div>
  </div>

  <div v-else class="bg-slate-800/30 p-6 rounded-xl border border-slate-700 text-center text-gray-400">
    Select a trade card to see details
  </div>
</template>

<script setup>
defineProps({
  item: { type: Object, default: null }
})
</script>

<style scoped>
</style>