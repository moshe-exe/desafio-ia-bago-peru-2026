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

**Container local + API key de IA = mockup competente.**

</div>

Lo demás es criterio.

---
layout: section
---

# Mapa del talk

1. **El método** — cómo organizar las 48h
2. **La arquitectura** — qué construir
3. **Los errores** — qué evitar

---
layout: section
---

# Parte 1 — El método

---

# La regla #1: recorta hasta que duela

> Si después de recortar el scope no sientes que perdiste algo importante, **no recortaste lo suficiente**.

<v-click>

### El antipatrón

"Vamos a hacer una plataforma que..."

### El patrón

"Vamos a hacer **una sola cosa**: que el usuario pueda *[acción concreta]* y reciba *[resultado concreto]*."

</v-click>

---

# Las 48 horas en 4 bloques

| Bloque | Horas | Objetivo |
|--------|-------|----------|
| **0. Decidir** | 0 – 4h | Reto elegido, "demo line" en una oración, lista explícita de lo que **NO** van a construir |
| **1. Esqueleto** | 4 – 20h | Container local + API + LLM + UI mínima → **end-to-end con dummies**, todo hardcoded. **Deploy en la hora 12.** |
| **2. Pulir lógica** | 20 – 36h | Iterar el corazón de la interacción (prompts, tools, flujo). Calidad solo sobre el *happy path*. |
| **3. Demo + pitch** | 36 – 48h | UI presentable, **grabar video backup**, ensayar pitch 3 veces |

---
layout: center
class: text-center
---

# Regla heurística

<div class="text-2xl mt-8">

> "Si en la hora 12 no tienes el end-to-end corriendo con dummies, **no es un problema de tecnología — es de scope**. No cambies de stack. Recorta más."

</div>

---

# Pivotar

Cambiar la dirección de tu solución cuando descubres que la actual no va a llegar.

<v-click>

**Duele.** Ya invertiste horas. Tu cerebro va a inventar razones para no hacerlo.

</v-click>

<v-click>

### Regla pragmática

**Pivotar antes de la hora 24 es barato. Después es caro.**

</v-click>

<v-click>

<div class="mt-8 text-lg italic opacity-80">

No te enamores de la primera idea. **Enamórate del problema, no de la solución.**

</div>

</v-click>

---
layout: two-cols
---

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
layout: section
---

# Parte 2 — La arquitectura

---

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

# Foundry — lo mínimo para 48h

| Concepto | Qué es | Para qué lo tocas |
|----------|--------|-------------------|
| **Project** | Contenedor de recursos | Tu workspace — uno por equipo |
| **Model** | Un LLM disponible (gpt-4o, gpt-4o-mini, o3-mini) | Eliges cuál deployar (recomiendo gpt-4o-mini) |
| **Deployment** | Un model con endpoint + quota | Lo que llamas desde tu código con la API key |
| **Connection** | Link a otro recurso | Solo si necesitas RAG / storage |
| **AI Search** | Index vectorial as-a-service | Raramente en 48h |

<div class="mt-4 text-sm opacity-70">
  <strong>No tocan:</strong> Evaluations, Fine-tuning, Content Safety policies, custom roles.
</div>

---

# Foundry — CLI > Consola

La consola está hecha para clickear y explorar. **En 48h, cada click te quita 15 segundos.**

```bash
az login
az ai project create --name desafio-equipo-N
az ai model deploy --model gpt-4o-mini --capacity 1
# endpoint listo en ~90 segundos
```

### Dos reglas con G&S

1. **Quota / permisos / accesos → al inge de G&S.** No peleen con la consola.
2. **Todo lo creativo (modelos, prompts, lógica) → CLI o SDK.**

---

# Agente vs Workflow · cómo se ve cada mockup

| | **Workflow** | **Agente** |
|---|---|---|
| **UI típica** | Formularios, botones, stepper "paso 2/4" | Chat libre + panel "thinking..." con tool calls |
| **Ejemplo healthcare** | Paciente loguea síntoma → eval contra reglas → respuesta | Médico pide *"resúmeme la última consulta"* → agente decide tools |
| **Cómo se ve la demo** | "Primero X, luego Y" — jurado entiende fácil | El "wow" es mostrar el razonamiento en vivo |
| **Trampa** | Requiere pensar bien el flow antes de codear | Jurado puede confundirse — hay que **mostrar el thinking** |

---

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
layout: section
---

# Parte 3 — Los errores

---

# Top 5 errores en hackatones de IA · salud

1. **Construir features en lugar de la demo.**<br/>
   <span class="opacity-70 text-sm">Ya saben — solo recordatorio. Cada feature que no se demuestra es horas perdidas.</span>

2. **Querer "datos médicos reales".**<br/>
   <span class="opacity-70 text-sm">Pierden 8h limpiando datasets. <strong>Pattern:</strong> hardcodea 3-5 perfiles únicos → mini-agente "redactor" genera un pool con reglas de realismo. 30 min vs 8h.</span>

3. **Multi-agente prematuro.**<br/>
   <span class="opacity-70 text-sm">Empiecen mono-agente. Especialicen y dividan <strong>solo cuando el mono-agente colapse</strong>. Casi nunca colapsa en 48h.</span>

4. **Olvidar al human-in-the-loop.**<br/>
   <span class="opacity-70 text-sm">En salud, la IA no decide. <em>"El agente sugiere medicación, el médico aprueba con un click."</em> No es nice-to-have — es <strong>atribuibilidad de responsabilidad</strong>.</span>

5. **Dejar el deploy para el final.**<br/>
   <span class="opacity-70 text-sm">Despliega en la hora 12. No en la hora 47.</span>

---

# Lo que SÍ ayuda

- 👤 **Una sola persona dueña de la demo.** Decide qué entra y qué no.
- 🎭 **Construye con dummies.** Hardcode + agente redactor donde necesites variedad.
- 🌳 **Trunk-based dev.** No hagan PRs entre ustedes. Commit directo a `main`.
- 📹 **Graba la demo en la hora 40.** Si el sistema falla en vivo, tienes el video.
- ⏱️ **Ensaya el pitch en voz alta 3+ veces.** El tiempo importa.

---
layout: center
class: text-center
---

# Recursos adicionales

Repo público con código de ejemplo, snippets y patterns:

<div class="mt-8 text-xl">

👉 [github.com/moshe-exe/desafio-ia-bago-peru-2026-recursos](https://github.com/moshe-exe/desafio-ia-bago-peru-2026-recursos)

</div>

<div class="mt-8 text-left max-w-md mx-auto opacity-90">

Incluye:
- 🔌 Llamada básica al modelo (Python + Node)
- 🛠️ Function calling / tool definition
- 🤖 Mini-agente con loop
- 🧪 Pattern: agente redactor de dummies

</div>

<div class="mt-6 text-sm opacity-60">

*(Pendiente de publicar — link final en la versión aprobada de la presentación.)*

</div>

---
layout: center
class: text-center
---

# Las 3 reglas que te van a salvar

<div class="text-2xl mt-8 space-y-4">

1. **Recorta el scope hasta que duela.**
2. **Construye el demo path, no el producto.**
3. **Despliega en la hora 12, no en la 47.**

</div>

---
layout: center
class: text-center
---

# Gracias

## ¿Preguntas?

<div class="mt-8 text-lg">

[github.com/moshe-exe](https://github.com/moshe-exe) · Agentman · Mentorium

</div>
