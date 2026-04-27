<template>
  <div class="min-h-screen flex flex-col scroll-smooth">
    <main class="grow flex w-full max-w-[1200px] flex-col items-center px-6 pt-24 pb-16">
      <header class="mb-16 flex w-full max-w-3xl flex-col items-center text-center">
        <h1 class="text-5xl md:text-7xl font-extrabold tracking-tight mb-6">
          <span class="gradient-text">JellyCC</span> CLI
        </h1>

        <h2 class="mb-6 font-display text-4xl font-semibold leading-tight md:text-5xl">
          Direct Play <br class="hidden md:block" /><span class="gradient-text">whenever possible.</span>
        </h2>

        <p class="mx-auto max-w-xl text-base leading-relaxed text-gray-400 md:text-lg">
          A CLI tool designed to optimize your media files for Jellyfin. Skip the transcode, keep the quality.
        </p>
      </header>

      <section class="group mb-24 w-full max-w-3xl">
        <div class="rounded-[16px] bg-linear-to-r from-primary/70 via-white/10 to-primary/30 p-px shadow-[0_0_40px_rgba(121,40,202,0.15)] transition-shadow duration-500 group-hover:shadow-[0_0_60px_rgba(255,0,128,0.25)]">
          <div class="overflow-hidden rounded-[15px] bg-surface">
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
                type="button"
                @click="copyInstallCmd"
                class="ml-4 flex-shrink-0 rounded-md border border-white/10 bg-white/5 p-2 text-gray-400 transition-colors hover:bg-white/10 hover:text-white focus:outline-hidden focus:ring-2 focus:ring-primary/50"
                title="Copiar comando"
                aria-label="Copiar comando de instalação"
              >
                <svg
                  class="h-4 w-4"
                  viewBox="0 0 16 16"
                  fill="none"
                  aria-hidden="true"
                  focusable="false"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M6 2.75h3.5A1.75 1.75 0 0 1 11.25 4.5V6H10V4.5a.25.25 0 0 0-.25-.25H6a.25.25 0 0 0-.25.25v1.25H4.5V4.5A1.75 1.75 0 0 1 6.25 2.75Z"
                    stroke="currentColor"
                    stroke-width="1.5"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                  />
                  <path
                    d="M5 4.75h5A1.75 1.75 0 0 1 11.75 6.5v5A1.75 1.75 0 0 1 10 13.25H5A1.75 1.75 0 0 1 3.25 11.5v-5A1.75 1.75 0 0 1 5 4.75Z"
                    stroke="currentColor"
                    stroke-width="1.5"
                    stroke-linejoin="round"
                  />
                </svg>
              </button>
            </div>
          </div>
        </div>
        <div 
          class="mt-3 text-center font-mono text-xs text-primary transition-opacity duration-300"
          :class="showCopyFeedback ? 'opacity-100' : 'opacity-0'"
          aria-live="polite"
          aria-atomic="true"
        >
          Copiado para a área de transferência!
        </div>
      </section>
    </main>

    <footer class="mt-auto w-full border-t border-white/10 bg-surface/50">
      <div class="mx-auto flex max-w-[1200px] flex-col items-center justify-between gap-4 px-6 py-8 md:flex-row">
        <div class="font-display text-xl font-bold text-white">
          JellyCC
        </div>
        <nav class="flex flex-wrap justify-center gap-6 font-mono text-[10px] uppercase tracking-widest text-gray-500 md:gap-8">
          <a href="https://github.com/parkejunior/jellycc-cli" class="transition-colors hover:text-primary" target="_blank" rel="noreferrer">Github</a>
        </nav>
        <div class="font-mono text-[10px] tracking-widest text-gray-600 uppercase">
          © 2026 JELLYCC.
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup lang="ts">
const installCommand = "curl -fsSL https://raw.githubusercontent.com/parkejunior/jellycc/main/install.sh | bash"
const showCopyFeedback = ref(false)
let copyFeedbackTimeout: ReturnType<typeof setTimeout> | undefined

const clearCopyFeedback = () => {
  if (copyFeedbackTimeout !== undefined) {
    clearTimeout(copyFeedbackTimeout)
    copyFeedbackTimeout = undefined
  }
}

const copyToClipboard = async (value: string) => {
  if (navigator.clipboard?.writeText) {
    await navigator.clipboard.writeText(value)
    return
  }

  const textarea = document.createElement("textarea")
  textarea.value = value
  textarea.setAttribute("readonly", "true")
  textarea.style.position = "fixed"
  textarea.style.opacity = "0"
  textarea.style.pointerEvents = "none"

  document.body.appendChild(textarea)
  textarea.select()

  const copied = document.execCommand("copy")
  document.body.removeChild(textarea)

  if (!copied) {
    throw new Error("Clipboard copy fallback failed")
  }
}

const copyInstallCmd = async () => {
  try {
    clearCopyFeedback()
    await copyToClipboard(installCommand)
    showCopyFeedback.value = true
    copyFeedbackTimeout = setTimeout(() => {
      showCopyFeedback.value = false
      copyFeedbackTimeout = undefined
    }, 1800)
  } catch (error) {
    console.error("Failed to copy install command", error)
  }
}

onBeforeUnmount(() => {
  clearCopyFeedback()
})
</script>
