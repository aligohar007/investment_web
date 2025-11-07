<template>
  <div
    class="bg-slate-800/50 backdrop-blur-sm p-6 rounded-xl border border-slate-700 hover:border-yellow-400/50 transition-all duration-300 transform hover:-translate-y-2 cursor-pointer h-full flex flex-col"
    @click="$emit('select', item)"
  >
    <div class="relative">
      <img
        v-if="item.image"
        :src="item.image"
        :alt="item.title"
        class="w-full h-36 object-cover rounded-md mb-4"
      />
      <div class="absolute top-2 right-2">
        <span class="px-2 py-1 bg-yellow-400 text-slate-900 rounded text-xs font-semibold">
          {{ type }}
        </span>
      </div>
    </div>

    <div class="flex-grow">
      <div class="text-yellow-400 text-2xl font-bold mb-1">{{ item.value }}</div>
      <h3 class="text-white text-lg font-semibold mb-2">{{ item.title }}</h3>
      <p class="text-gray-400 text-sm">{{ item.description }}</p>
    </div>

    <div class="mt-4 flex items-center justify-between border-t border-slate-700 pt-4">
      <span class="inline-flex items-center gap-2">
        <svg class="w-4 h-4 text-yellow-400" viewBox="0 0 24 24" fill="none" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"/>
        </svg>
        <span class="text-slate-300 text-sm">{{ item.origin || 'Global' }}</span>
      </span>
      <button
        class="px-3 py-1 bg-yellow-400 text-slate-900 rounded-md text-xs font-semibold hover:bg-yellow-500 transition-colors"
      >
        Details
      </button>
    </div>
  </div>
</template>

<script setup>
defineProps({
  item: {
    type: Object,
    required: true
  },
  type: {
    type: String,
    default: 'Import'
  }
})

defineEmits(['select'])
</script>

<style scoped>
.backdrop-blur-sm {
  backdrop-filter: blur(8px);
}
</style>