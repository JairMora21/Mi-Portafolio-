# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev        # Start dev server at localhost:4321
npm run build      # Type-check with astro check, then build to ./dist/
npm run preview    # Preview production build locally
```

There are no tests in this project.

## Stack

- **Astro 4** with file-based routing — pages in `src/pages/` map directly to routes
- **Tailwind CSS 3** via `@astrojs/tailwind` integration (config in [tailwind.config.mjs](tailwind.config.mjs))
- **Flowbite 2** — Tailwind component library; its plugin is registered in `tailwind.config.mjs` and its CDN script is loaded in the layout
- **TypeScript** in strict mode (`tsconfig.json` extends `astro/tsconfigs/strict`)
- **Onest Variable** font via `@fontsource-variable/onest`

## Architecture

The site is a static portfolio in Spanish. Content is hardcoded directly in component files — there is no CMS or content collection layer.

### Pages and layouts

| Route | Page file | Layout used |
|---|---|---|
| `/` | `src/pages/index.astro` | `Layout.astro` |
| `/adminrooms` | `src/pages/adminrooms.astro` | `LayoutProyects.astro` |
| `/soccerstats` | `src/pages/soccerstats.astro` | `LayoutProyects.astro` |

`Layout.astro` loads the global font, Flowbite CDN script, and wraps content with `Header` + `Footer`. `LayoutProyects.astro` is the same but tailored for project detail pages.

### Component responsibilities

- `src/components/Proyects.astro` — project cards on the homepage; links to the project detail pages
- `src/components/Experience.astro` — work experience timeline section
- `src/components/Estudios.astro` — education and certifications section
- `src/components/ProjectDetailAdmin.astro` / `ProjectDetailsSoccer.astro` — full project detail views (carousel, tech stack badges, YouTube embed)
- `src/components/SectionContainer.astro` — thin wrapper that applies consistent max-width and padding to each section
- `src/icons/` and `src/icons2/` — per-technology SVG icon components (one file per icon)

### Static assets

Project screenshots live under `public/AdminRooms/` and `public/SoccerStats/`. The profile photo is loaded from a LinkedIn CDN URL.

### Styling conventions

Dark theme is the only theme. Background is `neutral-950` with a purple radial gradient applied via inline style in the layout. Tailwind utility classes are used directly in markup; there are no custom CSS files. `darkMode: 'class'` is configured but the site does not implement a toggle — dark classes are applied statically.
