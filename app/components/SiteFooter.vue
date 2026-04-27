<template>
  <footer class="mt-auto w-full border-t border-white/10 bg-surface/50">
    <div class="mx-auto flex max-w-[1200px] flex-col items-center justify-between gap-4 px-6 py-8 md:flex-row">
      <div class="font-display text-xl font-bold text-white">
        JellyCC
      </div>

      <nav class="flex flex-wrap justify-center gap-6 font-mono text-[10px] uppercase tracking-widest text-gray-500 md:gap-8">
        <NuxtLink
          to="https://github.com/parkejunior/jellycc-cli"
          external
          target="_blank"
          rel="noreferrer"
          class="transition-colors hover:text-primary"
        >
          Github
        </NuxtLink>
      </nav>

      <div class="font-mono text-[10px] uppercase tracking-widest text-gray-600">
        © 2026 JELLYCC.
      </div>
    </div>
  </footer>
</template>
