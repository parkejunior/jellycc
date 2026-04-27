# AGENTS.md

## Project Overview

JellyCC is a small Nuxt 4 landing page for the JellyCC CLI. The app is a single-page marketing site with a hero section, install-command callout, and footer. The stack is Nuxt 4, Vue 3, and Tailwind CSS v4 via `@tailwindcss/vite`.

## Repository Layout

- `app/app.vue`: the main landing page. Most content and interaction live here.
- `app/assets/css/main.css`: global CSS, font imports, and shared theme helpers.
- `nuxt.config.ts`: Nuxt configuration, global CSS registration, and Vite/Tailwind wiring.
- `public/`: static assets such as `favicon.ico` and `robots.txt`.
- `.nuxt/`, `.output/`, and `.data/`: generated directories. Do not edit them by hand.
- `bun.lock`: Bun is the preferred package manager for this repo.

## Setup Commands

- Install dependencies: `bun install`
- Start the dev server: `npm run dev`
- Build for production: `npm run build`
- Preview the production build locally: `npm run preview`

Use Bun by default because the repository already has a `bun.lock` file. In this workspace, the npm script runner resolves the local Nuxt binary reliably, so prefer `npm run ...` for dev/build/preview commands.

## Development Workflow

- Keep landing-page changes focused in `app/app.vue` unless the work clearly needs a reusable component or a new route.
- Put shared styling in `app/assets/css/main.css` and prefer Tailwind utilities in templates for layout and spacing.
- If you need a new component, add it under `app/components/` and let Nuxt auto-import it.
- If you need a new page or route, add files under `app/pages/`.
- Restart the dev server after dependency or config changes.
- Keep the install command shown on the page aligned with the CLI repo or release flow it points to.

## Testing Instructions

- There is no dedicated test runner or lint script defined in `package.json` today.
- Use `npm run build` as the main verification step before handing off changes.
- If you add tests later, document the exact command here and make it easy to run from the repo root.

## Code Style

- Follow the existing Nuxt/Vue style: `<script setup lang="ts">`, composition API, and auto-imported Vue/Nuxt APIs.
- Match the surrounding formatting in each file instead of reformatting unrelated code.
- Keep the visual style consistent with the current design language: dark background, gradient accents, and bold typography.
- Prefer small, focused edits over broad rewrites in this landing page.
- Do not translate or rewrite marketing copy unless the task asks for it.

## Build and Deployment

- `npm run build` produces the production output in `.output/`.
- `npm run preview` serves the built app locally.
- Static files in `public/` are copied as-is into the build.
- There is no documented CI/CD workflow in this repo yet, so keep build and deployment steps simple and reproducible.

## Troubleshooting

- If Nuxt types or generated imports look stale, delete `.nuxt/` and rerun `npm run dev`.
- If Tailwind classes stop applying, confirm `app/assets/css/main.css` is still imported from `nuxt.config.ts`.
- If dependency resolution gets weird, rerun `bun install` instead of mixing package managers.
- If `bun run build` reports `nuxt: command not found`, use `npm run build` instead. That is the validated build path in this repository right now.

## PR / Handoff

- Before opening a PR or handing off work, run `npm run build`.
- Keep commits and changes scoped to the landing page unless the task explicitly expands the project.
- Call out any new environment variables, external assets, or third-party URLs in the handoff.
