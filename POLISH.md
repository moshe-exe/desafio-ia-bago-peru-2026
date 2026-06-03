# Polish — desafio-ia-bago-peru-2026

**Estado:** completed
**Iniciado:** 2026-06-03
**Última actualización:** 2026-06-03
**Slides totales:** 18
**Slides polished:** 14 / 18 (4 "no-changes" confirmed positive patterns)
**Criterios al momento:** 23 (C1-C13 + N1-N10) + 2 patrones positivos (P1, P2)
**Fase actual:** completed — Phase 1 (Tier A), Phase 2 (Tier B), iteración slides 12/14, N10 derivado. Tier C revisado y descartado (redundante/rechazado/out-of-scope).

Screenshots capturados con `npm run export -- --format png --output polish/` y renombrados a `NN-before.png`.

---

## Cola de slides

| # | Título | Estado | Fase |
|---|--------|--------|------|
| 01 | Cómo construir un producto de IA Generativa en menos de 48 horas | polished | Phase 1 |
| 02 | Quién soy | polished | Phase 1 |
| 03 | Qué les voy a contar | polished | Phase 1 |
| 04 | El objetivo | no-changes | (P1 confirmed) |
| 05 | Mapa del talk | polished | Phase 1 |
| 06 | La regla #1: recorta hasta que duela | polished | Phase 2 |
| 07 | Las 48 horas en 4 bloques | polished | Phase 1 |
| 08 | Cuándo cambiar de rumbo | polished | Phase 1 |
| 09 | Hardcode estratégico | polished | Phase 1 |
| 10 | Stack mínimo · mockup en 48h | polished | Phase 1 |
| 11 | Foundry — lo mínimo para 48h | no-changes | (P2 confirmed) |
| 12 | Foundry — CLI > Consola | polished | Phase 2 |
| 13 | Agente vs Workflow · cómo se ve cada mockup | no-changes | (P2 confirmed) |
| 14 | No es blanco o negro | polished | Phase 2 |
| 15 | El insight contraintuitivo | no-changes | — |
| 16 | Top errores · y cómo evitarlos | polished | Phase 1 |
| 17 | Las 3 reglas que te van a salvar | polished | Phase 2 |
| 18 | Gracias | polished | Phase 2 |

---

## Slides procesados

### Phase 1 — Tier A criteria (N1-N5) + low-risk slides

Pasada en modo paralelo (18 agentes), criterios consolidados, edits aplicados en una sola pasada.

**Slide 01 — Cover**
Antes: `polish/01-before.png` · Después: `polish/01-after.png`
Criterios: C4, C6, N1.
Edits: wrap en `<div class="h-full flex flex-col items-center justify-center text-center">`; subtítulo en peso uniforme (sin bold mixto).

**Slide 02 — Quién soy**
Antes: `polish/02-before.png` · Después: `polish/02-after.png`
Criterios: C1, C2, C6, C8, N1.
Edits: `layout: center`, `class: text-left`; body wrapped en `<div class="mt-6 pl-2 space-y-5 text-lg">` con inner `<div class="pl-4 space-y-4">`.

**Slide 03 — Qué les voy a contar**
Antes: `polish/03-before.png` · Después: `polish/03-after.png`
Criterios: C1, C2, C6, C8, N1.
Edits: `layout: center`, `class: text-left`; body en `<div class="mt-10 space-y-6 pl-4 max-w-4xl text-lg">`.

**Slide 05 — Mapa del talk**
Antes: `polish/05-before.png` · Después: `polish/05-after.png`
Criterios: C1, C2, C6, C8.
Edits: `layout: center`, `class: text-left`; lista en `<div class="mt-10 pl-6 space-y-5 text-lg">`.

**Slide 07 — Las 48 horas en 4 bloques**
Antes: `polish/07-before.png` · Después: `polish/07-after.png`
Criterios: C10, N3.
Edits: wrap en `<div class="slide-07-table mt-6">`; style.css `table-layout: fixed` + anchos 22%/13%/65% + `nowrap` cols 1-2 → tabla wrappea consistente a 2 líneas por celda.

**Slide 08 — Cuándo cambiar de rumbo**
Antes: `polish/08-before.png` · Después: `polish/08-after.png`
Criterios: C1, C2, C5, N2.
Edits: wrap en `<div class="h-full flex flex-col justify-center max-w-4xl">`; subtítulo "Dos checkpoints, dos reglas." en `text-base opacity-60 mb-10`; cada pregunta+respuesta en su propio `<div class="mb-10/12">` con gap interno `mt-2`.

**Slide 09 — Hardcode estratégico**
Antes: `polish/09-before.png` · Después: `polish/09-after.png`
Criterios: C1, C6, C9, N4.
Edits: layout cambiado de `two-cols` a manual CSS grid (`<div class="grid grid-cols-2 gap-12 mt-8">`); título h1 arriba compartido por ambas columnas; cola "El jurado no le da puntos..." span con `col-span-2`.

**Slide 10 — Stack mínimo · mockup en 48h**
Antes: `polish/10-before.png` · Después: `polish/10-after.png`
Criterios: C1.
Edits: wrap en `<div class="h-full flex flex-col justify-center">`.

**Slide 16 — Top errores · y cómo evitarlos**
Antes: `polish/16-before.png` · Después: `polish/16-after.png`
Criterios: C12, N5.
Edits: emojis ❌/✅ removidos; headers reemplazados por `<span class="th-err">Error</span>` y `<span class="th-fix">Cómo evitarlo</span>`; style.css con prefijos `× / ✓` inyectados via `::before`, colores `--c-primary` / `--c-fg`, peso 600.

---

### Slides sin cambios (confirmados)

- **Slide 04 — El objetivo:** P1 (`layout: center` + título chico + payoff grande). Funciona, mantener.
- **Slide 11 — Foundry — lo mínimo para 48h:** P2 (tabla 3-col balanceada). Mantener.
- **Slide 13 — Agente vs Workflow:** P2. Mantener.
- **Slide 15 — El insight contraintuitivo:** balanceado, v-click delay funciona. Mantener.

---

### Phase 2 — Tier B criteria (N6-N9)

Aplicados después de la revisión de Phase 1.

**Slide 06 — La regla #1: recorta hasta que duela**
Antes: `polish/06-before.png` · Después: `polish/06-after.png`
Criterios: C1, C2, C3, C5, N6.
Edits: wrap en `<div class="h-full flex flex-col justify-center max-w-5xl">`; callout con `mt-8 mb-10`; h3 "El antipatrón"/"El patrón" reemplazados por mini-labels en grid `label / value` (uppercase, tracking-widest, opacity-60).

**Slide 12 — Foundry — CLI > Consola**
Antes: `polish/12-before.png` · Después: `polish/12-after.png`
Criterios: C2, C5, C12, N7.
Edits: 📦 emoji removido; coletilla "— solo tienen que entender qué pedirle" cortada (N7); h3 "Dos reglas con G&S" reemplazado por mini-label uppercase tracking-widest (N6).

**Slide 14 — No es blanco o negro**
Antes: `polish/14-before.png` · Después: `polish/14-after.png`
Criterios: C1, C3, C7, N9.
Edits: layout cambiado a `two-cols`; col izq con diagrama + prompt diagnóstico + bullets de criterio agrupados (N9 — todo junto, no en reveal); col der con `v-click` revealing "salud zona gris".

**Slide 17 — Las 3 reglas que te van a salvar**
Antes: `polish/17-before.png` · Después: `polish/17-after.png`
Criterios: C1, C2, C11.
Edits: lista reescrita con estructura "titular bold en línea 1 / descripción no-bold en línea 2 indentada"; cada ítem en su propio div con `space-y-10`. Ritmo visual predecible, sin huérfanos.

**Slide 18 — Gracias**
Antes: `polish/18-before.png` · Después: `polish/18-after.png`
Criterios: C1, C6, C12, C13, N8.
Edits: 📦 removido; "## ¿Preguntas?" reemplazado por `<div class="text-2xl opacity-80">` (evita h2 compitiendo con h1); 3 bloques distintos en jerarquía descendente (toolkit / github personal / empresas).
