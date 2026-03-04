# TIL Blog

Blog minimalista de "Today I Learned" para Julio.

## Stack

- **Framework:** Astro 5 con Content Collections
- **Hosting:** Vercel (deploy automatico desde GitHub)
- **Repo:** https://github.com/Juliomperezd/til-blog

## Estructura

```
src/
├── content.config.ts          # Schema: title, date, tags, draft
├── content/til/               # Entradas Markdown
├── layouts/BaseLayout.astro   # Layout base (sin header ni footer)
├── components/TilCard.astro   # Card con hover gris
├── pages/
│   ├── index.astro            # Listado con titulo "TIL."
│   └── til/[slug].astro       # Pagina individual
└── styles/global.css          # Variables CSS
```

## Estilos

- **Tipografia display:** Syne (Google Fonts) — headlines, UI, branding
- **Tipografia mono:** JetBrains Mono (Google Fonts) — fechas, tags, código, prose
- **Fondo:** Blanco (#ffffff)
- **Texto:** Near-black (#0d0d0d)
- **Header y Footer:** activos con borde 2px negro

### Cards (index)
- Titulo: clamp(1.375rem, 3vw, 1.875rem), Syne bold, letter-spacing -0.03em
- Meta (fecha + tags): JetBrains Mono xs, uppercase
- Tags: outlined (border), sin fondo
- Hover: underline en titulo + flecha → animada

### Pagina interior
- Titulo: clamp(2.5rem, 8vw, 5.5rem), Syne 800, line-height 0.95, letter-spacing -0.04em
- Linea 2px negra bajo el titulo
- Back nav: mono xs uppercase
- Prose: JetBrains Mono 0.9375rem, line-height 1.85
- Subtitulos en prose: Syne bold 1.125rem

## Crear nueva entrada

```bash
touch src/content/til/YYYY-MM-DD-slug.md
```

Formato:
```markdown
---
title: "Titulo"
date: YYYY-MM-DD
tags: ["tag1", "tag2"]
---

Contenido...
```

## Comandos

```bash
npm run dev      # Desarrollo local (localhost:4321)
npm run build    # Build de produccion
git add -A && git commit -m "mensaje" && git push   # Subir cambios
```

## Notas

- Push a GitHub despliega automaticamente en Vercel
- Convención de nombres: `YYYY-MM-DD-slug.md`
- El campo `draft: true` oculta la entrada del listado
