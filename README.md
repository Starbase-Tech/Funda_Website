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
| `src/components/Pricing.astro` | Size-band pricing, term/year toggle, add-ons, terms. **Prices are set at the top of this file** |
| `src/components/Cta.astro` | Contact section — **email and WhatsApp number are set at the top of this file** |
| `src/assets/screens/` | App screenshots (optimised to WebP at build time) |

## Screenshots

The screenshots are real captures of the Funda web app with demo data (fictional "Riverview Primary School"). Replace files in `src/assets/screens/` with the same names to update them.

## Deploy

The site runs on **Cloudflare Workers** as the `funda-website` Worker, connected to this GitHub repo. It's served at `funda360.africa` and `www.funda360.africa`. Cloudflare's free plan allows commercial use.

### Releasing a change

1. Check it locally: `npm run dev`, then `npm run build` (the build must pass, or Cloudflare's will fail too).
2. Commit and push to `main`.
3. **That's it.** Cloudflare builds and deploys every push to `main` by itself. It takes 1–2 minutes.
4. Check: **Cloudflare dashboard → Workers & Pages → funda-website → Deployments** shows the build. Then open https://funda360.africa (hard refresh: Ctrl+Shift+R).

**Pushes to other branches** don't touch the live site. Each one gets a preview link on `*-funda-website.tapi-ndhlovu.workers.dev`, shown in Deployments. Use one to show a change before merging it into `main`.

### Rolling back

**Deployments** → pick the last good deployment → **⋯ → Rollback**. It's instant and needs no rebuild. Then fix the problem in git, because the next push to `main` deploys again.

### If a build fails

Open the failed deployment in **Deployments** and read the build log. It's usually something that also fails in `npm run build` locally. The live site keeps running the previous version until a build succeeds.

### How it was set up (once, 2026-10-26)

For reference, in case it ever has to be redone:

- **Workers & Pages → Create → Import a repository** → `Starbase-Tech/funda-website`, production branch `main`, build command `npm run build`.
- **Domains:** `funda360.africa` and `www.funda360.africa`, set to **Production only**. Never use "Production and Preview": previews would land on subdomains of funda360.africa, which belong to the schools (the `*` record → prod server).
- Before adding a domain, the old `@` (A) and `www` (CNAME) DNS records had to be deleted. Never touch the `api` or `*` records: they belong to the app.
