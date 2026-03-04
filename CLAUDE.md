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

- **Tipografia:** IBM Plex Mono (Google Fonts)
- **Fondo:** Blanco (#ffffff)
- **Sin header ni footer**

### Cards (index)
- Titulo: 40px, line-height 32px, letter-spacing -0.10em
- Espaciado fecha-titulo-tags: 16px
- Hover: fondo gris (#f5f5f5)

### Pagina interior
- Titulo: 88px, line-height 0.9, letter-spacing -0.06em
- Espaciado fecha-titulo-tags: 32px
- Parrafos: 14px
- Subtitulos (h2, h3...): 32px, letter-spacing -0.05em

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
