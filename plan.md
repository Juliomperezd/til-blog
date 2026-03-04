# Plan: Blog TIL con Astro + Vercel

## Resumen
Blog minimalista para entradas diarias "Today I Learned" usando Astro 5, desplegado en Vercel. Escribir una entrada = crear un archivo `.md` y hacer push.

## Stack
- **Framework:** Astro 5 (Content Collections)
- **Hosting:** Vercel (deploy automático desde GitHub)
- **Contenido:** Archivos Markdown en `src/content/til/`
- **Estilos:** CSS con variables personalizables

## Estructura del Proyecto

```
til-blog/
├── astro.config.mjs
├── package.json
├── src/
│   ├── content.config.ts       # Schema de TILs
│   ├── content/til/            # Entradas Markdown
│   │   └── YYYY-MM-DD-slug.md
│   ├── layouts/
│   │   └── BaseLayout.astro
│   ├── components/
│   │   └── TilCard.astro
│   ├── pages/
│   │   ├── index.astro         # Listado de TILs
│   │   └── til/[slug].astro    # Página individual
│   └── styles/
│       └── global.css          # Variables CSS personalizables
```

## Pasos de Implementación

### 1. Inicializar proyecto Astro
```bash
npm create astro@latest . -- --template minimal
```

### 2. Crear estructura de carpetas
- `src/content/til/` - Entradas TIL
- `src/layouts/` - Layout base
- `src/components/` - TilCard
- `src/styles/` - CSS global

### 3. Configurar Content Collections
Archivo `src/content.config.ts` con schema:
- `title`: string (requerido)
- `date`: fecha (requerido)
- `tags`: array de strings (opcional)
- `draft`: boolean (opcional)

### 4. Crear componentes
- **BaseLayout.astro**: HTML base, meta tags, importa CSS
- **TilCard.astro**: Tarjeta para listado (fecha, título, tags, hover gris)

### 5. Crear páginas
- **index.astro**: Lista todas las TILs ordenadas por fecha
- **til/[slug].astro**: Renderiza una entrada individual

### 6. Estilos
CSS con variables en `:root`:
- Fondo blanco
- Tipografía IBM Plex Mono
- Títulos grandes con letter-spacing ajustado

### 7. Deploy en Vercel
1. Inicializar git y crear repo en GitHub
2. Conectar repo en vercel.com
3. Vercel detecta Astro automáticamente

## Formato de Entrada TIL

```markdown
---
title: "Título de mi aprendizaje"
date: 2025-03-04
tags: ["tag1", "tag2"]
---

Contenido en Markdown...
```

**Convención de nombres:** `YYYY-MM-DD-slug.md`

## Flujo de Trabajo Diario

```bash
# Crear nueva entrada
touch src/content/til/2025-03-04-mi-aprendizaje.md

# Editar con tu editor favorito
# Commit y push -> Vercel despliega automáticamente
git add -A
git commit -m "Nueva entrada: mi aprendizaje"
git push
```

## Verificación

1. **Local:** `npm run dev` → abrir http://localhost:4321
2. **Build:** `npm run build` → verificar que no hay errores
3. **Deploy:** Push a GitHub → verificar URL de Vercel
4. **Nueva entrada:** Crear archivo .md → verificar que aparece en el listado
