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
├── components/TilCard.astro   # Card con flecha →
├── pages/
│   ├── index.astro            # Eyebrow + titulo TIL_ + listado de cards
│   └── til/[slug].astro       # Pagina individual
└── styles/global.css          # Variables CSS + prose styles
```

## Estilos

- **Tipografia:** JetBrains Mono para todo (display + mono)
- **Fondo:** Blanco (`#ffffff`)
- **Texto:** Near-black (`#0d0d0d`)
- **Accent:** `#0d0d0d` (sin colores de acento vivos)
- **Max width:** 780px
- **Border radius:** 8px (`--radius`)
- **Sin header ni footer**

### Index — Header

- Eyebrow: `~/aprendizajes` con dot pulsante (animacion `pulse 2.5s`)
- Titulo: `TIL_` con cursor parpadeante (`blink 1.1s step-end`)
- Tamaño titulo: `clamp(3.25rem, 9vw, 5.5rem)`, weight 800, letter-spacing -0.05em, line-height 0.95
- Divider horizontal debajo del header
- Animacion de entrada: `headerIn 0.5s cubic-bezier(0.16, 1, 0.3, 1)`

### Cards (index)

- Layout: columna, `min-height: 180px`, `justify-content: space-between`
- Padding: `32px 28px 28px`
- Fondo: `#ffffff`, border: `1px solid rgba(0,0,0,0.1)`
- Sin efecto hover especial (sin tilt 3D ni pokemon effect)
- Titulo: `clamp(1.5rem, 3.5vw, 2.1rem)`, weight 700, letter-spacing -0.03em
- Fecha: mono xs, uppercase, muted (`#888888`)
- Flecha `→` en esquina inferior derecha, color muted
- Animacion stagger: `cardIn 0.45s` con delay `index * 70ms`

### Pagina interior

- Back nav: `← volver`, mono xs uppercase, muted; hover cambia a accent
- Fecha: mono xs, capitalize, muted
- Tags: fondo `rgba(0,0,0,0.05)`, color `#0d0d0d`, border `rgba(56,189,248,0.2)`
- Titulo: `clamp(2.5rem, 8vw, 5.5rem)`, weight 800, line-height 0.95, letter-spacing -0.04em
- Animacion: `postIn 0.4s cubic-bezier(0.16, 1, 0.3, 1)`

### Prose

- JetBrains Mono, `0.9375rem`, line-height 1.85, color `#444444`
- Subtitulos: bold `1.125rem`, color `#0d0d0d`
- Code inline: fondo `#f0f0f0`, border `rgba(0,0,0,0.12)`
- Pre/code block: fondo `#f5f5f5`, border-left `2px solid #0d0d0d`
- Links: underline, `text-underline-offset: 3px`, color `#0d0d0d`

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

## Interactividad en posts (.md)

En Astro 5, dentro de un `.md` se puede escribir HTML, CSS y JS inline directamente. Esto permite playgrounds y visualizaciones sin dependencias externas.

### Patrón de playground (dark, estilo Día 2)

```html
<div class="dark-playground" id="pg-X">
  <span class="pg-hint">// hover</span>
</div>
<style>.dark-playground { height:260px; background:#09090f; border-radius:8px; ... }</style>
<script>(function(){ /* lógica IIFE */ })();</script>
```

### Patrón de visualización de datos (estilo Día 3)

Playgrounds oscuros (`#0d0d17`) con Canvas puro, sin librerías. Cada viz tiene:
- Header con label + segmented control (Día/Semana/Mes) estilo iOS
- Canvas area (`height: 258px`) con dibujo via Canvas 2D API
- Tooltip HTML posicionado absolutamente (`.viz-tt`)

**Helper `setupCanvas(canvasId, areaId)`** — gestiona DPR, resize y redraw:
- Retorna `{ canvas, ctx, area, resize, dpr(), onResize(fn) }`
- `onResize(fn)` registra callback que se llama tras cada ResizeObserver
- Primer render: `requestAnimationFrame(draw)` para esperar layout completo

**Helper `setupSegCtrl(segId, periods, onChange)`** — gestiona el filtro de período

**Patrón de animación entre períodos:**
```javascript
animFrom = currentVals();   // snapshot antes de cambiar
period = newPeriod;
animT = 0; animStart = performance.now();
requestAnimationFrame(draw); // draw() lee animT y hace lerp con ease()
```

**Paleta de colores viz:**
- Primary: `#7c6ff7` (purple)
- Secondary: `#4ade80` (green)
- Tertiary: `#f59e0b` (amber), `#ef4444` (red), `#60a5fa` (blue)
- Fondo playground: `#0d0d17`
- Fondo widget: `#131320`
- Grid lines: `rgba(255,255,255,0.05)`
- Texto muted: `rgba(255,255,255,0.28)`

### Patrón de widget grid (estilo Día 3, inspirado en iPhone Weather)

Grid 4×2 de widgets cuadrados (`aspect-ratio: 1`) con Canvas:
- `wSetup(canvasId, wrapId, drawFn)` — helper simplificado para widgets
- Cada widget: `.widget` > `.w-lbl` + `.ww` (wrapper relativo) > `canvas` + `.viz-tt`
- Sin filtro de período, con hover tooltip

**8 tipos implementados:** sparkline, gauge semicírculo, heatmap dots, scatter, big stat + sparkline, horizontal bars rankeadas, ring único, EQ bars coloreadas por valor

### Reglas canvas importantes

- Siempre usar `devicePixelRatio` para nitidez en Retina
- `ctx.setTransform(dpr, 0, 0, dpr, 0, 0)` tras cada resize (resetea la escala)
- Dibujar en coordenadas CSS (no device pixels)
- `canvas.width = area.clientWidth * dpr` + `canvas.style.width = area.clientWidth + 'px'`
- Primer `draw()` via `requestAnimationFrame` — el canvas puede tener dims 0 si se llama sync

## Notas

- Push a GitHub despliega automaticamente en Vercel
- Convencion de nombres: `YYYY-MM-DD-slug.md`
- El campo `draft: true` oculta la entrada del listado
- `Header.astro` y `Footer.astro` existen en components pero no se usan
