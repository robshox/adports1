## Project snapshot
- This repo is a Next.js 15 App Router app using React 19 and server components by default (see `src/app/layout.tsx`).
- Styling relies on Tailwind CSS v4 with CSS custom properties defined in `src/app/globals.css` for light/dark themes.

## File layout
- `src/app/layout.tsx` sets fonts via `next/font` (Geist) and exposes metadata; export new metadata in this file.
- `src/app/page.tsx` is currently the only route; new routes belong under `src/app/<segment>/page.tsx`.
- Shared utilities live in `src/lib`, e.g., `src/lib/utils.ts` exports `cn` for class merging; reuse it instead of manual string joins.
- Static assets live in `public/`; reference them via `/asset.svg` paths when using `next/image`.

## Styling conventions
- Tailwind is imported through `@import "tailwindcss"`; use class names directly, and prefer design tokens declared under `@theme inline`.
- Dark mode toggles by applying the `.dark` class at the `<html>` root; ensure new components read colors from the CSS variables (`bg-background`, `text-foreground`).
- When combining classes, pass arrays to `cn(...)` so `tailwind-merge` removes conflicts (e.g., `cn("grid", conditional && "hidden")`).

## Component patterns
- Default to server components; add `"use client"` only when you need hooks or browser-only APIs.
- Use `next/image` for images (see `src/app/page.tsx`) and always provide `width`, `height`, and `alt`.
- For icons, prefer `lucide-react`; it's already installed even if not yet used.

## Developer workflow
- Install deps with `npm install` (lockfile is npm).
- Run locally with `npm run dev`; build with `npm run build`; start production build via `npm run start`.
- Lint with `npm run lint`; fix issues as result because the CI template expects an eslint-clean tree.

## Extending the app
- Update `next.config.ts` if you introduce external domains for images or need experimental flags.
- When adding themes or variants, adjust the custom properties in `globals.css` and keep the `@theme inline` definitions in sync.
- Document new utilities in `README.md` or extend these instructions so future AI agents understand the workflow.
