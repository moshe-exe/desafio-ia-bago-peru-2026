---
theme: seriph
title: Cómo construir un producto de IA Generativa en menos de 48 horas
info: |
  ## Desafío IA Bagó Perú 2026
  Charla por Moshe Ojeda · UPC Campus Monterrico · 12 de junio 2026.
class: text-center
highlighter: shiki
drawings:
  persist: false
transition: slide-left
mdc: true
---

<div class="cover-slide h-full flex flex-col items-center justify-center text-center">

# Cómo construir un producto<br/>de IA Generativa en menos de 48 horas

<div class="mt-10 text-lg opacity-75 tracking-wide">

Desafío IA Bagó Perú 2026 · Moshe Ojeda · 12 jun 2026

</div>

</div>

<div class="abs-br m-6 text-xl">
  <a href="https://github.com/moshe-exe/desafio-ia-bago-peru-2026" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

---
layout: center
class: text-left
---

# Quién soy

<div class="mt-6 pl-2 space-y-5 text-lg">

**Moshe Ojeda**

<div class="pl-4 space-y-4">

Soy **cofundador de Agentman**, donde desplegamos agentes para **healthcare**.

Y también **cofundador de Mentorium**, donde ofrecemos **IA para instituciones educativas**.

</div>

</div>

---
layout: center
class: text-left
---

# Qué les voy a contar

<div class="mt-10 space-y-6 pl-4 max-w-4xl text-lg">

Voy a contarles, muy concretamente, **qué haría yo si estuviera en su lugar** estas 48 horas.

**Por qué** tomaría cada decisión.

Y **cómo aplico esto mismo en mi día a día** en Agentman y Mentorium.

</div>

---
layout: center
class: text-center
---

<div class="flex justify-center mb-6">
  <IconBadge shape="squircle" size="lg"><div class="i-ph:target" /></IconBadge>
</div>

# El objetivo

<div class="text-3xl mt-8 mb-8">

**Mockup competente en 48 horas.**

</div>

Lo demás es criterio.

---
layout: center
class: text-left
---

# Mapa del talk

<div class="mt-10 pl-6 space-y-5 text-lg">

1. **El método** — cómo organizar las 48h
2. **La arquitectura** — qué construir
3. **Los errores** — qué evitar

</div>

---

<div class="abs-tr m-4 text-xs opacity-40 font-mono">Parte 1 · El método</div>

<div class="h-full flex flex-col justify-center max-w-5xl">

<div class="flex items-center gap-4">
  <IconBadge shape="squircle" size="md"><div class="i-ph:scissors" /></IconBadge>
  <h1 class="!m-0">La regla #1: recorta hasta que duela</h1>
</div>

<div class="mt-8 mb-10">

> Si después de recortar el scope no sientes que perdiste algo importante, **no recortaste lo suficiente**.

</div>

<v-click>

<div class="grid grid-cols-[auto_1fr] gap-x-8 gap-y-6 mt-4 items-baseline">

<div class="text-sm uppercase tracking-widest opacity-60">Antipatrón</div>
<div>"Vamos a hacer una plataforma que…"</div>

<div class="text-sm uppercase tracking-widest opacity-60">Patrón</div>
<div>"Vamos a hacer <strong>una sola cosa</strong>: que el usuario pueda <em>[acción concreta]</em> y reciba <em>[resultado concreto]</em>."</div>

</div>

</v-click>

</div>

---

<div class="abs-tr m-4 text-xs opacity-40 font-mono">Parte 1 · El método</div>

# Las 48 horas en 4 bloques

<div class="slide-07-table mt-6">

| Bloque | Horas | Objetivo |
|--------|-------|----------|
| **0. Decidir** | 0 – 4h | Reto elegido, "demo line" en una oración, lista explícita de lo que **NO** van a construir |
| **1. Esqueleto** | 4 – 20h | Container local + API + LLM + UI mínima → **end-to-end con dummies**, todo hardcoded. **Deploy en la hora 12.** |
| **2. Pulir lógica** | 20 – 36h | Iterar el corazón de la interacción (prompts, tools, flujo). Calidad solo sobre el *happy path*. |
| **3. Demo + pitch** | 36 – 48h | UI presentable, **grabar video backup**, ensayar pitch 3 veces |

</div>

---

<div class="abs-tr m-4 text-xs opacity-40 font-mono">Parte 1 · El método</div>

<div class="h-full flex flex-col justify-center max-w-4xl">

<div class="flex items-center gap-4">
  <IconBadge shape="squircle" size="md"><div class="i-ph:compass" /></IconBadge>
  <h1 class="!m-0">Cuándo cambiar de rumbo</h1>
</div>

<div class="text-base opacity-60 mt-3 mb-10">Dos checkpoints, dos reglas.</div>

<v-click>

<div class="mb-10">

**Hora 12 — ¿corre el end-to-end con dummies?**

<div class="mt-2 opacity-90">

Si **NO** → no es problema de tecnología, es de **scope**. Recorta más. No cambies de stack.

</div>

</div>

</v-click>

<v-click>

<div class="mb-12">

**Hora 24 — ¿la dirección sigue viable?**

<div class="mt-2 opacity-90">

Si **NO** → **pivota**. Duele — ya invertiste horas — pero pivotar antes de la hora 24 es barato. Después es caro.

</div>

</div>

</v-click>

<v-click>

<div class="mt-4 text-lg italic opacity-75 text-center">

No te enamores de la primera idea. **Enamórate del problema, no de la solución.**

</div>

</v-click>

</div>

---

<div class="abs-tr m-4 text-xs opacity-40 font-mono">Parte 1 · El método</div>

<div class="flex items-center gap-4">
  <IconBadge shape="squircle" size="md"><div class="i-ph:wrench" /></IconBadge>
  <h1 class="!m-0">Hardcode estratégico</h1>
</div>

<div class="grid grid-cols-2 gap-12 mt-8">

<div>

**Hardcodea lo que no aporta a la demo.**

- IDs de usuario
- Datos de entrada de ejemplo
- Resultados intermedios "no-IA"
- Configuración

</div>

<div>

**Construye de verdad lo que vende la idea.**

- La interacción central con el modelo
- El prompt + tools + memoria
- El output que el jurado va a ver
- El flujo que cuentas en el pitch

</div>

<div class="col-span-2 mt-6 text-sm opacity-70 text-center">
  El jurado no le da puntos a tu sistema de auth.
</div>

</div>

---

<div class="abs-tr m-4 text-xs opacity-40 font-mono">Parte 2 · La arquitectura</div>

<div class="h-full flex flex-col justify-center">

# Stack mínimo · mockup en 48h

| Capa | Qué usar |
|------|----------|
| **Frontend** | Lo más simple — Streamlit, una página HTML, lo que sea |
| **Backend** | FastAPI o Express en container local |
| **LLM** | `gpt-4o-mini` en Azure AI Foundry |
| **Datos** | Dummies en JSON / SQLite / archivos |
| **Deploy** | Local primero. Azure Container Apps si llegan. |

<v-click>

<div class="mt-6 text-sm opacity-70">
  <strong>Regla:</strong> elige el stack que ya conoces. El hackatón no es para aprender Kubernetes.
</div>

</v-click>

</div>

---

<div class="abs-tr m-4 text-xs opacity-40 font-mono">Parte 2 · La arquitectura</div>

# Foundry — lo mínimo para 48h

| Concepto | Qué es | Para qué lo tocas |
|----------|--------|-------------------|
| **Project** | Contenedor de recursos | Tu workspace — uno por equipo |
| **Model** | Un LLM disponible (gpt-4o, gpt-4o-mini, o3-mini) | Eliges cuál deployar (recomiendo gpt-4o-mini) |
| **Deployment** | Un model con endpoint + quota | Lo que llamas desde tu código con la API key |
| **Connection** | Link a otro recurso | Solo si usan AI Search o Blob. Si no, no la toquen. |
| **AI Search** | Index vectorial as-a-service | Overkill en 48h. Pásenle los datos directamente al modelo. |

<div class="mt-4 text-sm opacity-70">
  <strong>No tocan:</strong> Evaluations, Fine-tuning, Content Safety policies, custom roles.
</div>

---

<div class="abs-tr m-4 text-xs opacity-40 font-mono">Parte 2 · La arquitectura</div>

# Foundry — CLI > Consola

<div class="mt-6 space-y-2">

La consola está hecha para clickear. **En 48h, cada click te quita 15 segundos.**

¿No dominan `az`? **Pídanselo a un agente de código** — Claude, Cursor o Copilot lo manejan por ustedes.

</div>

<div class="mt-10">

```bash
az login
az extension add -n cognitiveservices
# crear resource group → Foundry → deployar gpt-4o-mini
```

<div class="mt-2 text-sm opacity-90">

Snippet completo + skill de Claude para Foundry: [**github.com/moshe-exe/ai-mockup-quickstart**](https://github.com/moshe-exe/ai-mockup-quickstart)

</div>

</div>

<div class="mt-12">

<div class="text-sm uppercase tracking-widest opacity-60">Dos reglas con G&S</div>

<div class="mt-3 space-y-2">

1. **Quota, permisos, accesos → al inge de G&S.** No peleen con la consola.
2. **Todo lo creativo → CLI o SDK.**

</div>

</div>

---

<div class="abs-tr m-4 text-xs opacity-40 font-mono">Parte 2 · La arquitectura</div>

# Agente vs Workflow · cómo se ve cada mockup

| | **Workflow** | **Agente** |
|---|---|---|
| **UI típica** | Formularios, botones, stepper "paso 2/4" | Chat libre + panel "thinking..." con tool calls |
| **Ejemplo healthcare** | Paciente loguea síntoma → eval contra reglas → respuesta | Médico pide *"resúmeme la última consulta"* → agente decide tools |
| **Cómo se ve la demo** | "Primero X, luego Y" — jurado entiende fácil | El "wow" es mostrar el razonamiento en vivo |
| **Trampa** | Requiere pensar bien el flow antes de codear | Jurado puede confundirse — hay que **mostrar el thinking** |

---
layout: two-cols
---

<div class="abs-tr m-4 text-xs opacity-40 font-mono">Parte 2 · La arquitectura</div>

<div class="h-full flex flex-col justify-center pr-8">

<div class="flex items-center gap-4">
  <IconBadge shape="squircle" size="md"><div class="i-ph:circle-half" /></IconBadge>
  <h1 class="!m-0">No es blanco o negro</h1>
</div>

<div class="mt-8">

<div class="flex items-center text-lg font-mono">
  <span class="font-bold">Workflow</span>
  <div class="flex-1 mx-3 border-t-2 border-current opacity-60"></div>
  <span class="font-bold">Agente</span>
</div>

<div class="mt-2 flex justify-between text-xs opacity-70 italic">
  <span>("loguear síntoma")</span>
  <span>("explica mi diagnóstico")</span>
</div>

</div>

<div class="mt-10">

Pregúntate: *"¿Qué decisión tiene que tomar mi sistema?"*

<div class="mt-3 space-y-1">

- Si cabe en un `if/else` → **workflow**
- Si cambia según el contexto → **agente**

</div>

</div>

</div>

::right::

<v-click>

<div class="h-full flex flex-col justify-center pl-8 text-sm space-y-3">

<div class="text-xs uppercase tracking-widest opacity-60">La zona gris (en salud)</div>

En la mayoría de casos, el extremo correcto es obvio. Pero **en salud, la zona gris aparece seguido**:

<div class="space-y-1">

- una decisión puede ser **clínica** (estructurada) y **conversacional** (ambigua) a la vez,
- el input del paciente llega libre, pero la respuesta no puede serlo,
- la auditabilidad pesa.

</div>

<div class="italic opacity-85">

Cuando te encuentres ahí, **no la sobrepienses**. El siguiente slide te va a sesgar.

</div>

</div>

</v-click>

---
layout: center
class: text-center
---

<div class="abs-tr m-4 text-xs opacity-40 font-mono">Parte 2 · La arquitectura</div>

<div class="flex justify-center mb-6">
  <IconBadge shape="squircle" size="lg"><div class="i-ph:lightbulb" /></IconBadge>
</div>

# El insight contraintuitivo

<div class="text-xl mt-8 space-y-4">

**Workflow** = óptimo, pero más código de orquestación.

**Agente** = overkill, pero el **LLM se encarga de orquestar**.

</div>

<v-click>

<div class="mt-12 text-2xl">

En 48 horas, **"menos código que escribir"**<br/>gana a **"más óptimo en producción"**.

</div>

</v-click>

---

<div class="abs-tr m-4 text-xs opacity-40 font-mono">Parte 3 · Los errores</div>

<div class="flex items-center gap-4">
  <IconBadge shape="squircle" size="md"><div class="i-ph:warning" /></IconBadge>
  <h1 class="!m-0">Top errores · y cómo evitarlos</h1>
</div>

<div class="errors-table mt-8">

| <span class="th-err">Error</span> | <span class="th-fix">Cómo evitarlo</span> |
|----------|------------------|
| Construir **features** en vez de la demo | **Una sola persona** dueña de la demo |
| Querer **"datos médicos reales"** | **Dummies + agente redactor** (30 min vs 8h) |
| **Multi-agente prematuro** | Empieza **mono-agente**, especializa después |
| Olvidar al **human-in-the-loop** | *"El agente sugiere, el médico aprueba con un click"* |
| **Deploy tarde** | **Deploy en la hora 12**, no en la 47 |

</div>

<div class="mt-8 text-sm opacity-70 text-center">
  Otros: trunk-based dev · graba video backup en hora 40 · ensaya el pitch 3 veces
</div>

---
layout: center
class: text-center
---

<div class="flex justify-center mb-6">
  <IconBadge shape="squircle" size="lg"><div class="i-ph:lifebuoy" /></IconBadge>
</div>

# Las 3 reglas que te van a salvar

<div class="mt-12 text-left max-w-3xl mx-auto space-y-10">

<div>

**1. Recorta con cabeza, aunque duela.**

<div class="text-base opacity-80 mt-1 pl-6">

El miedo al dolor no es razón para no decidir bien.

</div>

</div>

<div>

**2. Tu demo es lo que sobrevive al recorte.**

<div class="text-base opacity-80 mt-1 pl-6">

Construye eso, nada más.

</div>

</div>

<div>

**3. El deploy de la hora 12 no es para mostrar.**

<div class="text-base opacity-80 mt-1 pl-6">

Es para descubrir lo que no funciona mientras todavía hay tiempo.

</div>

</div>

</div>

---
layout: center
class: text-center
---

# Gracias

<div class="mt-6 text-2xl opacity-80">¿Preguntas?</div>

<div class="mt-16 text-base">

Toolkit + skill de Claude para Foundry<br/>
[github.com/moshe-exe/ai-mockup-quickstart](https://github.com/moshe-exe/ai-mockup-quickstart)

</div>

<div class="mt-10 text-lg">

[github.com/moshe-exe](https://github.com/moshe-exe)

</div>

<div class="mt-4 text-base opacity-80">

Agentman · Mentorium

</div>
