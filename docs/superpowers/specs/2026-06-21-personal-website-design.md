# Personal Website — Design Spec

**Date**: 2026-06-21  
**Status**: Approved

## Overview

A personal website to introduce Mark, showcase programming projects, display photography, and present skills. Multi-page, elegant design, contemporary tech stack.

## Tech Stack

- **Framework**: Astro (static site generation, zero JS by default)
- **Styling**: Tailwind CSS
- **Deployment**: Vercel or Netlify (free tier)
- **Data**: JSON files for projects and photos (no CMS, no database)

## Site Map

```
/
├── /                Home — hero intro, quick navigation highlights
├── /projects        Projects — compact card grid, JSON-driven
├── /photography     Photography — gallery, JSON-driven, friendly tone
└── /about           About — balanced professional + personal
```

## Data Structures

### `src/data/photos.json`
Array of photo objects. Images stored in `/public/images/photography/`.
```json
{
  "filename": "sunset-over-city.jpg",
  "title": "Sunset Over City",
  "alt": "Golden hour skyline",
  "category": "landscape"
}
```
Adding a photo: drop file in `/public/images/photography/`, add entry to JSON. Site rebuilds with new content.

### `src/data/projects.json`
Array of project objects.
```json
{
  "name": "Project Name",
  "description": "One-liner summary of what it does.",
  "tags": ["TypeScript", "React", "Node.js"],
  "github": "https://github.com/...",
  "live": "https://...",
  "image": "project-thumb.jpg"
}
```

## Components

| Component | File | Purpose |
|-----------|------|---------|
| Layout | `src/layouts/Layout.astro` | Shell: nav + slot + footer |
| Nav | `src/components/Nav.astro` | Sticky top bar, mobile hamburger |
| ProjectCard | `src/components/ProjectCard.astro` | Compact card: image, name, description, tag pills, links |
| PhotoCard | `src/components/PhotoCard.astro` | Thumbnail that opens lightbox on click |
| SkillBadge | `src/components/SkillBadge.astro` | Small pill/badge for tech tags |
| Lightbox | `src/components/Lightbox.astro` | Full-screen photo viewer with prev/next, close |

## Visual Design

### Typography
- **Headings**: Serif (Playfair Display or Lora) — elegance and personality
- **Body**: Sans-serif (Inter or DM Sans) — professional, readable

### Color Palette
- **Background**: Warm off-white / cream (`#fafaf7` or similar)
- **Text**: Deep charcoal (`#292929`)
- **Accent**: One restrained color (muted slate blue or warm ochre) for links, tag pills, highlights
- Monochrome base with a single accent — no heavy gradients

### Spacing
- Generous whitespace, airy sections
- Narrow content width for text pages
- Full-width for photography gallery
- Thin rules/borders to separate sections

### Motion
- Fade-up on scroll for cards (subtle, not flashy)
- Smooth lightbox open/close for photos
- Clean, fast page transitions

### Tone
- Tech pages (projects, skills): professional, structured, slightly darker lean
- Photography: lighter, warmer, more breathing room, friendly captions

## Pages

### Home (`/`)
- Short greeting/intro line
- Personal photo or tasteful image
- Three navigation cards: Projects, Photography, About Me
- Subtle scroll indication

### Projects (`/projects`)
- Grid of ProjectCard components, 2-3 columns
- Each card: optional thumbnail, project name, one-line description, tech tag pills, GitHub/live links
- Read order from JSON

### Photography (`/photography`)
- Full-width justified grid or masonry of PhotoCard thumbnails
- Click opens Lightbox: large image, prev/next arrows, title, friendly caption
- Optional category filter at top (from JSON `category` field)

### About (`/about`)
- Intro paragraph: who Mark is, what he does (professional but approachable)
- Skills section: programming languages and tools, displayed as SkillBadge pills or clean list
- Personal touch: brief mention of photography and interests (warmer tone)
- Optional contact link

## Build & Development

- `npm run dev` — Astro dev server with hot reload
- `npm run build` — static site generation to `/dist`
- `npm run preview` — preview the built site locally

## Out of Scope

- CMS or database backend
- User authentication
- Commenting system
- Blog
