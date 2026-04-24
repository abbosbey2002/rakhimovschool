# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static HTML website for **Rahimov School** — a private school in Tashkent and Farg'ona, Uzbekistan. No build system, no bundler, no package manager. Open HTML files directly in a browser.

## File Structure

| File | Purpose |
|---|---|
| `index.html` | Main landing page (~2600 lines) |
| `team.html` | Teachers/staff page |
| `articles.html` | Blog/articles listing with client-side category filter |
| `contact.html` | Contact page with branch cards + Yandex Maps iframes |
| `Copywriting.MD` | Source of truth for all Uzbek copy/content |
| `assets/img/noroot.png` | School logo (used in all navbars + footers) |
| `assets/img/DSC03244.jpeg` | School photo |

## Tech Stack

- **Tailwind CSS** — CDN Play (JIT), configured inline via `tailwind.config` in each file's `<head>`. Arbitrary values like `w-[148px]` work.
- **Vanilla JS** — all logic is inline `<script>` blocks at the bottom of each file. No modules, no imports.
- **Yandex Maps** — embedded as iframes in `contact.html` using `map-widget/v1/` with `ll=lng,lat` parameter.

## Design System (shared across all pages)

**Brand colors** (defined in every file's `tailwind.config`):
```
brand-500: #07CA68  (primary green)
brand-600: #05b35b
brand-700: #04924a
brand-50/100: light green tints
```

**Typography**: `font-family: 'HelveticaNeueCyr', 'Helvetica Neue', Arial, sans-serif` — set in `<body>` CSS and Tailwind `fontFamily` extension as both `heading` and `body`.

**Scroll reveal animations**: Four CSS classes drive entrance animations via a shared `IntersectionObserver` pattern (threshold 0.12):
- `.reveal` — fade up
- `.reveal-left` / `.reveal-right` — slide in from sides
- `.reveal-scale` — scale up from 0.94

**Count-up numbers**: Elements with `data-count="76" data-suffix="+"` are animated by a second `IntersectionObserver` (threshold 0.5) that runs a 1500ms interval.

## Navbar Pattern (shared)

Every page has the same navbar structure. Dropdowns use `toggleDropdown(id)` which looks for `#${id}-panel` and `#${id}-chevron`. The lang switcher uses id `lang`, so its elements are `#lang-panel`, `#lang-chevron`, `#lang-current`. Clicking outside any `.nav-dropdown` closes all panels.

The phone button is an expanding hover element: idle = `w-9` icon only, hover = `w-[148px]` with "78 113 0005" sliding in.

## index.html Section Order

Loading screen → Header → Hero → Yutuqlar/Statistika → Maktab haqida → Darsdan tashqari faoliyat → Qabul jarayoni → Narxlar/Stipendiyalar → O'qituvchilar → Mijozlar fikri (video) → Galereya → CTA banner → Aloqa/Ariza form → Maqolalar preview → FAQ → Footer

## Key Patterns

**Forms** (`handleForm`): Fake submission — disables the button, shows `#successMsg` after 1s timeout. No actual backend.

**articles.html filtering**: Article cards have `data-category="ielts|sat|kitob|stipendiya|talim"`. `filterArticles(cat)` toggles `hidden` class and updates active filter button styles.

**contact.html branch cards**: Two Toshkent branches (Lokomotiv + Ibn Sino) each have a Yandex iframe (`ll=longitude,latitude&z=16`) with a custom school pin overlay centered via `absolute inset-0 flex items-center justify-center`. The pin is a CSS teardrop (green circle + triangle) with coordinate label.

**team.html card pattern**: `aspect-square + overflow-hidden + rounded-full` for initials avatars. Grid sections: Rahbariyat (3 col), Ingliz tili (4 col), Matematika (3 col), Boshqa fanlar (4 col).
