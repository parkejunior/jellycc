<template>
  <section class="group w-full max-w-3xl">
    <div class="rounded-[16px] bg-linear-to-r from-primary/70 via-white/10 to-primary/30 p-px shadow-[0_0_40px_rgba(121,40,202,0.15)] transition-shadow duration-500 group-hover:shadow-[0_0_60px_rgba(255,0,128,0.25)]">
      <div class="overflow-hidden rounded-[15px] bg-surface">
        <div class="flex items-center border-b border-white/5 px-4 py-3">
          <div class="flex space-x-2">
            <div class="h-3 w-3 rounded-full bg-white/20"></div>
            <div class="h-3 w-3 rounded-full bg-white/20"></div>
            <div class="h-3 w-3 rounded-full bg-white/20"></div>
          </div>
          <div class="ml-4 font-mono text-[11px] uppercase tracking-widest text-gray-500">
            install.sh
          </div>
        </div>

        <div class="relative px-5 py-5 font-mono text-sm sm:text-base">
          <div class="overflow-x-auto pr-16 sm:pr-20">
            <div class="flex min-w-max items-center whitespace-nowrap text-gray-300">
              <span class="mr-3 font-bold text-primary">&gt;</span>
              <span>{{ installCommand }}</span>
            </div>
          </div>

          <button
            type="button"
            @click="copyInstallCmd"
            class="absolute right-5 top-1/2 flex-shrink-0 -translate-y-1/2 rounded-md border border-white/10 bg-zinc-950 p-2 text-gray-400 shadow-lg shadow-black/20 transition-colors hover:bg-zinc-900 hover:text-white focus:outline-hidden focus:ring-2 focus:ring-primary/50 cursor-pointer"
            title="Copiar comando"
            aria-label="Copiar comando de instalação"
          >
            <IconsClipboardSvg />
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
</template>

<script setup lang="ts">
const installCommand = "curl -fsSL https://raw.githubusercontent.com/parkejunior/jellycc-cli/main/install.sh | bash"
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
