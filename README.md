# BVS VENTILATION – bvsventilation.se

Statisk webbplats byggd med [Astro](https://astro.build) och vanlig CSS. Driftsatt på Cloudflare (Workers static assets).

## Kommandon

| Kommando          | Vad den gör                                  |
| ----------------- | -------------------------------------------- |
| `npm install`     | Installerar beroenden (kräver Node 22.12+)   |
| `npm run dev`     | Utvecklingsserver på http://localhost:4321   |
| `npm run build`   | Bygger sajten till `dist/`                   |
| `npm run preview` | Förhandsgranskar den byggda sajten           |

## Struktur

- `src/pages/` – `index.astro` (/), `omoss/`, `tjanster/`, `kontakt/` och `404.astro`. Alla URL:er har avslutande snedstreck.
- `src/layouts/Layout.astro` – header, meny, footer, canonical, Open Graph och förladdning av typsnitt.
- `src/components/` – `Cta.astro` ("Vi finns här för dig!"), `ServiceCards.astro`, `Arrow.astro`.
- `src/data/services.ts` – tjänsterna (startsidan och /tjanster/).
- `src/styles/global.css` – all CSS, färger och typsnitt som variabler överst.
- `src/assets/` – logotyp och bilder (optimeras vid build till AVIF/WebP).
- `public/` – favicon, `og-image.jpg`, `robots.txt`, `_headers`, `_redirects`.
- `wrangler.jsonc` – Cloudflare-konfiguration.

## Redigera text
Ändra texten direkt i respektive `.astro`-fil. Varje sida har `title` och `description` (max ca 155 tecken, unik per sida) överst. Tjänstetexter finns i `src/data/services.ts`. Företagsuppgifter för Google (JSON-LD) finns i `src/pages/index.astro`, och adress/telefon i footern finns i `src/layouts/Layout.astro`.

## Redigera bilder
Lägg bilden i `src/assets/images/` (använd originalet i full storlek, Astro skapar mindre varianter), importera den i sidan och använd `<Picture src={bild} alt="Svensk beskrivning" />`. Bilder under första skärmen laddas lazy automatiskt; sätt `loading="eager"` bara på bilden högst upp. Open Graph-bilden byts genom att ersätta `public/og-image.jpg` (1200×630).

## Kontaktformulär
`/kontakt/` skickar med `fetch` till Formspree (`https://formspree.io/f/mrpelaak`, anges överst i `src/pages/kontakt/index.astro`). Svenska felmeddelanden visas per fält, knappen är avstängd under sändning och ett fält `_gotcha` fungerar som honeypot. Utan JavaScript skickas formuläret som en vanlig POST till Formspree.

## Driftsättning (Cloudflare)
Sajten använder Workers static assets:

- **Deploy command:** `npx wrangler deploy`
- **Build command:** `npm run build`
- **Output:** `dist/` (styrs av `assets.directory` i `wrangler.jsonc`)
- **Node:** Cloudflare behöver Node 22. Sätt miljövariabeln `NODE_VERSION` = `22` (Settings → Variables and Secrets → Build). Filen `.node-version` i repot anger också 22.

`public/_headers` ger säkerhetsheaders och långtidscache för `/_astro/*`. `public/_redirects` pekar gamla WordPress-adresser till rätt sida. Sidor som inte finns visar `404.astro`.

Efter byte av domän: koppla `bvsventilation.se` under Settings → Domains & Routes, och skicka in `https://bvsventilation.se/sitemap-index.xml` i Google Search Console.