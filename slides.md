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

# Cómo construir un producto de IA Generativa<br/>en menos de 48 horas

**Desafío IA Bagó Perú 2026** · Moshe Ojeda · 12 jun 2026

<div class="abs-br m-6 text-xl">
  <a href="https://github.com/moshe-exe/desafio-ia-bago-peru-2026" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

---

# Quién soy

**Moshe Ojeda**

Soy **cofundador de Agentman**, donde desplegamos agentes para **healthcare**.

Y también **cofundador de Mentorium**, donde ofrecemos **IA para instituciones educativas**.

---

# Qué les voy a contar

Voy a contarles, muy concretamente, **qué haría yo si estuviera en su lugar** estas 48 horas.

**Por qué** tomaría cada decisión.

Y **cómo aplico esto mismo en mi día a día** en Agentman y Mentorium.

---
layout: center
class: text-center
---

# El objetivo

<div class="text-3xl mt-8 mb-8">

**Mockup competente en 48 horas.**

</div>

Lo demás es criterio.

---

# Mapa del talk

1. **El método** — cómo organizar las 48h
2. **La arquitectura** — qué construir
3. **Los errores** — qué evitar

---

<div class="abs-tr m-4 text-xs opacity-40 font-mono">Parte 1 · El método</div>

# La regla #1: recorta hasta que duela

> Si después de recortar el scope no sientes que perdiste algo importante, **no recortaste lo suficiente**.

<v-click>

### El antipatrón

"Vamos a hacer una plataforma que..."

### El patrón

"Vamos a hacer **una sola cosa**: que el usuario pueda *[acción concreta]* y reciba *[resultado concreto]*."

</v-click>

---

<div class="abs-tr m-4 text-xs opacity-40 font-mono">Parte 1 · El método</div>

# Las 48 horas en 4 bloques

| Bloque | Horas | Objetivo |
|--------|-------|----------|
| **0. Decidir** | 0 – 4h | Reto elegido, "demo line" en una oración, lista explícita de lo que **NO** van a construir |
| **1. Esqueleto** | 4 – 20h | Container local + API + LLM + UI mínima → **end-to-end con dummies**, todo hardcoded. **Deploy en la hora 12.** |
| **2. Pulir lógica** | 20 – 36h | Iterar el corazón de la interacción (prompts, tools, flujo). Calidad solo sobre el *happy path*. |
| **3. Demo + pitch** | 36 – 48h | UI presentable, **grabar video backup**, ensayar pitch 3 veces |

---

<div class="abs-tr m-4 text-xs opacity-40 font-mono">Parte 1 · El método</div>

# Cuándo cambiar de rumbo

**Dos checkpoints, dos reglas:**

<v-click>

**Hora 12 — ¿corre el end-to-end con dummies?**

Si **NO** → no es problema de tecnología, es de **scope**. **Recorta más.** No cambies de stack.

</v-click>

<v-click>

**Hora 24 — ¿la dirección sigue viable?**

Si **NO** → **pivota.** Duele — ya invertiste horas — pero **pivotar antes de la hora 24 es barato. Después es caro.**

</v-click>

<v-click>

<div class="mt-8 text-lg italic opacity-80 text-center">

No te enamores de la primera idea. **Enamórate del problema, no de la solución.**

</div>

</v-click>

---
layout: two-cols
---

<div class="abs-tr m-4 text-xs opacity-40 font-mono">Parte 1 · El método</div>

# Hardcode estratégico

**Hardcodea lo que no aporta a la demo.**

- IDs de usuario
- Datos de entrada de ejemplo
- Resultados intermedios "no-IA"
- Configuración

::right::

**Construye de verdad lo que vende la idea.**

- La interacción central con el modelo
- El prompt + tools + memoria
- El output que el jurado va a ver
- El flujo que cuentas en el pitch

<div class="mt-6 text-sm opacity-70">
  El jurado no le da puntos a tu sistema de auth.
</div>

---

<div class="abs-tr m-4 text-xs opacity-40 font-mono">Parte 2 · La arquitectura</div>

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

La consola está hecha para clickear. **En 48h, cada click te quita 15 segundos.**

¿No dominan `az`? **Pídanselo a un agente de código.** Claude / Cursor / Copilot lo maneja por ustedes — solo tienen que entender qué pedirle.

```bash
az login
az extension add -n cognitiveservices
# crear resource group → Foundry → deployar gpt-4o-mini
```

📦 Snippet completo + skill de Claude para Foundry:
[**github.com/moshe-exe/ai-mockup-quickstart**](https://github.com/moshe-exe/ai-mockup-quickstart)

### Dos reglas con G&S

1. **Quota, permisos, accesos → al inge de G&S.** No peleen con la consola.
2. **Todo lo creativo → CLI o SDK.**

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

<div class="abs-tr m-4 text-xs opacity-40 font-mono">Parte 2 · La arquitectura</div>

# No es blanco o negro

<div class="text-center text-xl mt-4 mb-4 font-mono">

Workflow ━━━━━━━━━━━━━━━━━━━━━━ Agente

</div>

<div class="text-center text-sm opacity-70 mb-8">

↑ evidente · *("loguear síntoma")*   |   ↑ evidente · *("explica mi diagnóstico")*

</div>

Para arrancar, pregúntate: *"¿Qué decisión tiene que tomar mi sistema?"*

- Si cabe en un `if/else` → **workflow**
- Si cambia según el contexto → **agente**

<v-click>

En la mayoría de casos, el extremo correcto es obvio.

Pero **en salud, la zona gris aparece seguido**:
- una decisión puede ser **clínica** (estructurada) y **conversacional** (ambigua) a la vez,
- el input del paciente llega libre, pero la respuesta no puede serlo,
- la auditabilidad pesa.

Cuando te encuentres ahí, **no la sobrepienses**. El siguiente slide te va a sesgar.

</v-click>

---
layout: center
class: text-center
---

<div class="abs-tr m-4 text-xs opacity-40 font-mono">Parte 2 · La arquitectura</div>

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

# Top errores · y cómo evitarlos

| ❌ Error | ✅ Cómo evitarlo |
|----------|------------------|
| Construir **features** en vez de la demo | **Una sola persona** dueña de la demo |
| Querer **"datos médicos reales"** | **Dummies + agente redactor** (30 min vs 8h) |
| **Multi-agente prematuro** | Empieza **mono-agente**, especializa después |
| Olvidar al **human-in-the-loop** | *"El agente sugiere, el médico aprueba con un click"* |
| **Deploy tarde** | **Deploy en la hora 12**, no en la 47 |

<div class="mt-6 text-sm opacity-70 text-center">
  Otros: trunk-based dev · graba video backup en hora 40 · ensaya el pitch 3 veces
</div>

---
layout: center
class: text-center
---

# Las 3 reglas que te van a salvar

<div class="text-xl mt-8 space-y-6 text-left max-w-3xl mx-auto">

1. **Recorta con cabeza, aunque duela.** El miedo al dolor no es razón para no decidir bien.

2. **Tu demo es lo que sobrevive al recorte.** Construye eso, nada más.

3. **El deploy de la hora 12 no es para mostrar** — es para descubrir lo que no funciona mientras todavía hay tiempo.

</div>

---
layout: center
class: text-center
---

# Gracias

## ¿Preguntas?

<div class="mt-8 text-base">

📦 Toolkit + skill de Claude para Foundry:<br/>
[github.com/moshe-exe/ai-mockup-quickstart](https://github.com/moshe-exe/ai-mockup-quickstart)

</div>

<div class="mt-8 text-lg">

[github.com/moshe-exe](https://github.com/moshe-exe) · Agentman · Mentorium

</div>
