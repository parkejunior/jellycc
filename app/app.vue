<template>
  <div class="min-h-screen flex flex-col scroll-smooth items-center">
    <main class="grow flex w-full max-w-[1200px] flex-col items-center px-6 pt-24 pb-16 justify-center">
      <LandingHero />
      <InstallCommandCard />

      <div class="flex flex-col sm:flex-row items-center justify-center gap-4 w-full sm:w-auto">
        <ActionLink href="https://github.com/parkejunior/jellycc-cli">
          <font-awesome-icon icon="fa-brands fa-github" /> Github
        </ActionLink>

        <ActionLink href="https://buymeacoffee.com/parkejunior" variant="secondary">
          <font-awesome-icon icon="fa-solid fa-mug-hot" class="text-yellow-300" /> Buy me a coffee
        </ActionLink>
      </div>
    </main>

    <SiteFooter />
  </div>
</template>
