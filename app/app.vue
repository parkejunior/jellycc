<template>
  <div class="min-h-screen flex flex-col scroll-smooth">
    <main class="flex-grow w-full max-w-[1200px] mx-auto px-6 pt-24 pb-16 flex flex-col items-center">
        
      <header class="text-center w-full max-w-3xl flex flex-col items-center mb-16">
        <h1 class="text-5xl md:text-7xl font-extrabold tracking-tight mb-6">
            <span class="gradient-text">JellyCC</span> CLI
        </h1>

        <h2 class="font-space font-semibold text-4xl md:text-5xl leading-tight mb-6">
          Direct Play <br class="hidden md:block"/><span class="gradient-text">whenever possible.</span>
        </h2>

        <p class="font-inter text-gray-400 text-base md:text-lg max-w-xl mx-auto leading-relaxed">
          A CLI tool designed to optimize your media files for Jellyfin. Skip the transcode, keep the quality.
        </p>
      </header>

      <section class="w-full max-w-3xl mb-24 group">
        <div class="gradient-border-wrapper relative shadow-[0_0_40px_rgba(121,40,202,0.15)] transition-shadow duration-500 group-hover:shadow-[0_0_60px_rgba(255,0,128,0.25)]">
          <div class="bg-[#0a0a0c] rounded-[15px] overflow-hidden">
            <div class="flex items-center px-4 py-3 border-b border-white/5">
              <div class="flex space-x-2">
                <div class="w-3 h-3 rounded-full bg-white/20"></div>
                <div class="w-3 h-3 rounded-full bg-white/20"></div>
                <div class="w-3 h-3 rounded-full bg-white/20"></div>
              </div>
              <div class="ml-4 font-mono text-[11px] text-gray-500 uppercase tracking-widest">
                install.sh
              </div>
            </div>
            <div class="px-5 py-5 flex items-start sm:items-center justify-between font-mono text-sm sm:text-base overflow-x-auto relative">
              <div class="flex items-center whitespace-nowrap text-gray-300">
                <span class="text-primary mr-3 font-bold">></span>
                <span>{{ installCommand }}</span>
              </div>
              <button 
                @click="copyInstallCmd" 
                class="ml-4 p-2 rounded-md bg-white/5 hover:bg-white/10 text-gray-400 hover:text-white transition-colors border border-white/10 flex-shrink-0 focus:outline-none focus:ring-2 focus:ring-primary/50" 
                title="Copiar Comando"
              >
                <Copy class="w-4 h-4" />
              </button>
            </div>
          </div>
        </div>
        <div 
          class="text-center text-primary font-mono text-xs mt-3 transition-opacity duration-300"
          :class="showCopyFeedback ? 'opacity-100' : 'opacity-0'"
        >
          Copiado para a área de transferência!
        </div>
      </section>
    </main>

    <footer class="w-full border-t border-white/10 mt-auto bg-[#0a0a0c]/50">
      <div class="max-w-[1200px] mx-auto px-6 py-8 flex flex-col md:flex-row items-center justify-between gap-4">
        <div class="font-space font-bold text-xl text-white">
          JellyCC
        </div>
        <nav class="flex flex-wrap justify-center gap-6 md:gap-8 font-mono text-[10px] tracking-widest text-gray-500 uppercase">
          <a href="https://github.com/parkejunior/jellycc-cli" class="hover:text-primary transition-colors" target="_blank">Github</a>
        </nav>
        <div class="font-mono text-[10px] tracking-widest text-gray-600 uppercase">
          © 2026 JELLYCC.
        </div>
      </div>
    </footer>

    <svg style="width:0;height:0;position:absolute;" aria-hidden="true" focusable="false">
      <linearGradient id="primary-gradient" x1="0%" y1="0%" x2="100%" y2="100%">
        <stop offset="0%" stop-color="#FF0080" />
        <stop offset="100%" stop-color="#7928CA" />
      </linearGradient>
      <linearGradient id="secondary-gradient" x1="0%" y1="0%" x2="100%" y2="100%">
        <stop offset="0%" stop-color="#7928CA" />
        <stop offset="100%" stop-color="#FF0080" />
      </linearGradient>
    </svg>
  </div>
</template>

<script setup lang="ts">
const installCommand = "curl -fsSL https://raw.githubusercontent.com/parkejunior/jellycc/main/install.sh | bash"
const copyInstallCmd = () => {
}
const showCopyFeedback = ref(false)
</script>