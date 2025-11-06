<template>
  <div class=" bg-slate-800/50 backdrop-blur-sm p-6 rounded-xl border border-slate-700 hover:border-yellow-400/50 transition-all duration-300 transform hover:-translate-y-2 h-full">
    <div class=" text-yellow-400 text-3xl md:text-4xl font-bold mb-3">
      {{ item.value }}
    </div>
    <h3 class="text-white text-lg md:text-xl font-semibold mb-2">{{ item.title }}</h3>
    <p class="text-gray-400 text-sm md:text-base">{{ item.description }}</p>
  </div>
</template>

<script setup>
defineProps({
  item: {
    type: Object,
    required: true
  }
})
</script>

<style scoped>
/* visual tweaks handled via Tailwind utility classes in template */
</style>