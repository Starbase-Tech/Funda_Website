# Funda Website

Marketing site for [Funda](https://funda360.africa) — school management for Zimbabwean schools.

Built with [Astro](https://astro.build). Static output, no client framework — interactions are small vanilla TypeScript scripts inside each component.

## Develop

```bash
npm install
npm run dev       # http://localhost:4321
npm run build     # outputs to dist/
npm run preview   # serve the built site
```

## Structure

| Path | What it is |
|------|-----------|
| `src/pages/index.astro` | The page — assembles the sections below |
| `src/components/Hero.astro` | Animated receipt → Funda dashboard |
| `src/components/Replaces.astro` | "What Funda replaces" strike-through band |
| `src/components/Tour.astro` | Sticky-scroll product tour with real screenshots |
| `src/components/Roles.astro` | Interactive "who sees what" permission switcher |
| `src/components/Bento.astro` | Live feature cards (currency, verification, audit, year end…) |
| `src/components/Cta.astro` | Contact section — **email and WhatsApp number are set at the top of this file** |
| `src/assets/screens/` | App screenshots (optimised to WebP at build time) |

## Screenshots

The screenshots are real captures of the Funda web app with demo data (fictional "Riverview Primary School"). Replace files in `src/assets/screens/` with the same names to update them.

## Deploy

Any static host works. On Vercel or Netlify: build command `npm run build`, output directory `dist`.
