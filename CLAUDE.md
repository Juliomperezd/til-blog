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
├── components/TilCard.astro   # Card blanca con hover gris
├── pages/
│   ├── index.astro            # Titulo TIL. + listado de cards
│   └── til/[slug].astro       # Pagina individual
└── styles/global.css          # Variables CSS
```

## Estilos

- **Tipografia:** JetBrains Mono para todo (display + mono)
- **Fondo:** Blanco (#ffffff)
- **Texto:** Near-black (#0d0d0d)
- **Sin header ni footer**

### Cards (index)
- Titulo blog: clamp(2.75rem, 6vw, 3.75rem), weight 800, encima de las cards
- Titulo card: clamp(1.375rem, 3vw, 1.875rem), weight 700, letter-spacing -0.03em
- Fecha: JetBrains Mono xs, uppercase, muted
- Fondo default: blanco (#ffffff)
- Fondo hover: #F0F0F0, transicion 0.35s ease
- Padding: 24px arriba/abajo, 16px lados
- Border radius: 10px

### Pagina interior
- Back nav: mono xs uppercase, muted
- Fecha: mono xs uppercase, muted
- Titulo: clamp(2.5rem, 8vw, 5.5rem), weight 800, line-height 0.95, letter-spacing -0.04em
- Prose: JetBrains Mono 0.9375rem, line-height 1.85
- Subtitulos en prose: JetBrains Mono bold 1.125rem

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
