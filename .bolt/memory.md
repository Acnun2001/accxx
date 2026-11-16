# Project memory

## Product intent & audience

- Conversion-focused quiz funnel (28-step) for a weight-loss/health program
- Primary audience: Brazilian Portuguese (root `/`); secondary: Spanish/LATAM (`/lat`)
- Funnel stages: landing → age/body questions → weight goals → loading screens → results → testimonials → checkout offer → FAQ

## Brand personality & voice

- Direct, conversion-oriented tone with social proof (testimonials) and urgency-driven checkout

## Visual design & UX direction

- React SPA, single `index.html` per locale (~442KB minified JS embedded)
- Build pipeline: `build.cjs` copies source files to `dist/` (`index.html`, `assets/`, `metodo/`, `lat/`)
- Images stored in `assets/`; subfolder pages reference via `../assets/`
- Meta Pixel tracking integrated with anti-clone access gate

## Decisions, constraints & rationale

- Spanish (`/lat`) is a full clone of the main funnel with all UI text translated
- Currency: Portuguese version uses R$ (BRL); Spanish version uses € (EUR)
- Date locale: `pt-BR` for Portuguese, `es-ES` for Spanish
- Anti-clone redirect: points to `/metodo/` (PT) or `/lat/` (ES) depending on locale
- Meta Pixel `<noscript>` tag must be placed in `<body>` (before `#root`), not `<head>` — invalid HTML5 was breaking the page and the access gate
- Translation done via scripted string replacement on minified JS; 147 of 217 replacements applied, some strings may not have matched exactly

## Open questions & assumptions

- Some Portuguese strings may remain untranslated in `/lat` due to exact-match failures in minified code
- Purpose/content of `/metodo/` page not fully documented — appears to be the gated offer page for the Portuguese funnel
- Whether additional LATAM locales or currencies beyond EUR are planned