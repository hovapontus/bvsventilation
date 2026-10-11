# BVS VENTILATION – bvsventilation.se

Statisk webbplats byggd med [Astro](https://astro.build) och vanlig CSS. Hostas på Cloudflare Pages.

## Kommandon

| Kommando          | Vad den gör                              |
| ----------------- | ---------------------------------------- |
| `npm install`     | Installerar beroenden (Node 22.12+)      |
| `npm run dev`     | Startar utvecklingsserver på localhost:4321 |
| `npm run build`   | Bygger sajten till `dist/`               |
| `npm run preview` | Förhandsgranskar den byggda sajten       |

## Struktur

- `src/pages/` – sidorna: `index.astro` (/), `omoss/`, `tjanster/`, `kontakt/`. URL:erna har avslutande snedstreck.
- `src/layouts/Layout.astro` – gemensam header, meny, footer och SEO/Open Graph-taggar.
- `src/components/` – `Cta.astro` ("Vi finns här för dig!"), `ServiceCards.astro`, `Arrow.astro`.
- `src/data/services.ts` – tjänsterna (används på startsidan och /tjanster/).
- `src/styles/global.css` – all CSS; färger och typsnitt överst som CSS-variabler.
- `src/assets/` – logotyp och bilder (optimeras automatiskt vid build till AVIF/WebP).
- `public/` – favicon, `og-image.jpg`, `robots.txt`.

## Ändra text
Redigera texten direkt i respektive `.astro`-fil. Sidtitel och meta-beskrivning anges som `title` och `description` överst i varje sida. Tjänstetexter finns i `src/data/services.ts`.

## Ändra bilder
Lägg den nya bilden i `src/assets/images/`, importera den i sidan (`import x from '../assets/images/x.webp'`) och använd `<Picture src={x} alt="..." />`. Använd gärna originalbilden i full storlek – Astro skapar de mindre varianterna. Byt Open Graph-bilden genom att ersätta `public/og-image.jpg` (1200×630).

## Kontaktformulär
Formuläret på `/kontakt/` skickas med `fetch` till Formspree. Formspree-ID:t (`mrpelaak`) anges överst i `src/pages/kontakt/index.astro`. Fältet `_gotcha` är ett dolt honeypot-fält mot spam.

## Cloudflare Pages
Framework preset: Astro · Build command: `npm run build` · Output directory: `dist` · miljövariabel `NODE_VERSION` = `22`.
