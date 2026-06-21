# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal website for Mark — software engineer and photographer. Built with Astro and Tailwind CSS, deployed to GitHub Pages.

## Commands

```bash
npm run dev        # Start dev server with hot reload
npm run build      # Build static site to dist/
npm run preview    # Preview the built site locally
```

## Architecture

- **Framework**: Astro (static site generation, zero JS by default)
- **Styling**: Tailwind CSS with custom theme (colors, fonts in `tailwind.config.mjs`)
- **Deployment**: GitHub Pages via GitHub Actions (`.github/workflows/deploy.yml`)
- **Data**: JSON-driven content — edit `src/data/photos.json` or `src/data/projects.json` to update content

## Project Structure

```
src/
├── components/     # Reusable Astro components
│   ├── Nav.astro          # Sticky nav, desktop + mobile hamburger
│   ├── ProjectCard.astro  # Compact card: name, description, tag pills, links
│   ├── PhotoCard.astro    # Thumbnail, opens Lightbox on click
│   ├── SkillBadge.astro   # Tech tag pill
│   └── Lightbox.astro     # Full-screen photo viewer (vanilla JS)
├── layouts/
│   └── Layout.astro       # HTML shell: nav + slot + footer, IntersectionObserver for fade-up
├── pages/
│   ├── index.astro        # Home — hero intro, 3 nav cards
│   ├── projects.astro     # Project card grid, reads projects.json
│   ├── photography.astro  # Photo gallery grid, reads photos.json
│   └── about.astro        # Intro, skills (SkillBadge pills), contact
├── data/
│   ├── projects.json      # Array of {name, description, tags, github, live, image}
│   └── photos.json        # Array of {filename, title, alt, category}
├── styles/
│   └── global.css         # Tailwind directives, Google Fonts, custom component classes
└── env.d.ts               # Astro client type reference
public/
└── images/
    └── photography/       # Photo files referenced by photos.json
```

## Key Patterns

- **Content updates**: Edit `src/data/*.json` and rebuild — no CMS needed. Photos: drop files in `public/images/photography/`, add entries to `photos.json`.
- **Styling**: Utility-first with Tailwind. Custom classes (`.card`, `.pill`, `.fade-up`, `.nav-link`) defined in `global.css` `@layer components`.
- **Interactivity**: Vanilla JS in page-scoped `<script>` tags — no React/Vue islands. Mobile nav toggle and lightbox are the only interactive elements.
- **Fade-up animation**: Elements with `.fade-up` are observed by `IntersectionObserver` in `Layout.astro`. Add `.visible` class when they enter the viewport.
- **GitHub Pages base path**: The `base` in `astro.config.mjs` is `/Personal_Website`. All internal links use relative paths (Astro handles this).
- **Design tone**: Tech pages (projects, about skills) — professional, structured. Photography page — warmer, friendly captions. Serif headings (Playfair Display), sans-serif body (Inter).
