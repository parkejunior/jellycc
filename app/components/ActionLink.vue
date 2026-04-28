<template>
  <a 
    :href="href" 
    target="_blank"
    :class="[
      'w-full sm:w-auto px-8 py-3.5 rounded-xl font-bold text-lg tracking-wide hover:scale-[1.02] transition-all duration-200 cursor-pointer flex items-center justify-center gap-2',
      variant === 'primary' 
        ? 'bg-gradient-to-r from-pink-500 to-purple-600 text-white hover:opacity-90 shadow-lg' 
        : 'bg-zinc-800 text-zinc-100 hover:bg-zinc-700 border border-zinc-700/50'
    ]"
  >
    <slot />
  </a>
</template>

<script setup>
defineProps({
  href: {
    type: String,
    required: true
  },
  variant: {
    type: String,
    default: 'primary',
    validator: (value) => ['primary', 'secondary'].includes(value)
  }
})
</script>