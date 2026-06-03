# Revisiones — desafio-ia-bago-peru-2026

**Estado:** `review-1`
**Rondas completadas:** 1
**Mínimo para aprobar:** 2
**Última actualización:** 2026-06-02

> No publicable hasta completar al menos 2 rondas. Falta 1 ronda.

---

## Ronda 1 — 2026-06-02

**Foco:** reemplazar el contenido placeholder (que era mi mejor intento) por contenido real basado en el brief de Bagó, el contexto de healthcare confirmado con Simon Amador, y la voz pragmática de Moshe.

### Cambios aplicados

**Identidad y framing (slides 2-4)**
- Slide 2 ("Quién soy"): eliminado Yape, Rappi, "10+ años". Reemplazado por frase clave: *"Soy cofundador de Agentman, donde desplegamos agentes para healthcare, y también cofundador de Mentorium, donde ofrecemos IA para instituciones educativas."*
- Slide 3 ("Qué les voy a contar"): reemplazado framing genérico de "sí pero producto no significa MVP" por framing pragmático: *"voy a contarles qué haría yo si estuviera en su lugar, por qué, y cómo aplico esto en mi día a día."*
- Slide 4 ("El objetivo"): nuevo slide ancla técnica — *"Container local + API key de IA = mockup competente. Lo demás es criterio."*

**Método (slides 6-9)**
- Slide 7 ("Las 48h en 4 bloques"): rediseñados sin "datos reales" (confirmado con Simon: el evento espera esqueleto+dummies). Nuevos bloques: 0-4h Decidir / 4-20h Esqueleto / 20-36h Pulir lógica / 36-48h Demo+pitch. Incluye "deploy en la hora 12".
- Slide 8 ("Regla heurística"): nueva regla provisional — *"Si en la hora 12 no tienes el end-to-end corriendo con dummies, no es problema de tecnología, es de scope. Recorta más."*
- Slide 9 ("Pivotar"): nuevo slide. Reconoce el peso emocional del pivote. Regla pragmática: pivotar antes de la hora 24 es barato, después es caro.

**Arquitectura (slides 11-15)**
- Slide 11 ("Stack mínimo"): rediseñado para mockup en 48h con foco en `gpt-4o-mini` en Foundry y deploy local primero.
- Slide 12 ("Foundry — lo mínimo"): nueva tabla con Project / Model / Deployment / Connection / AI Search. Explícitamente NO incluye: Evaluations, Fine-tuning, Content Safety, custom roles.
- Slide 13 ("Foundry — CLI > Consola"): nuevo. Comandos `az` + dos reglas con G&S (quota a inge, creativo en CLI/SDK).
- Slide 14 ("Agente vs Workflow A — mockups"): expandido de 1 slide a 3. Tabla comparativa lado a lado con ejemplos healthcare.
- Slide 15 ("Agente vs Workflow B — espectro"): nuevo slide bridge. Espectro visual + reconocimiento de zona gris frecuente en salud (decisión clínica + conversacional, input libre + respuesta no, auditabilidad).
- Slide 16 ("Agente vs Workflow C — insight contraintuitivo"): nuevo. *"Workflow = más óptimo, más código. Agente = overkill, menos código. En 48h, menos código gana."*

**Errores (slides 18-19)**
- Slide 18 ("Top 5 errores"): completamente reformulado para healthcare.
  - 1. Features vs demo (breve, sobreentendido)
  - 2. Querer datos médicos "reales" → reemplazado con pattern del agente redactor de dummies
  - 3. Multi-agente prematuro → empezar mono-agente, especializar después
  - 4. NUEVO: Olvidar human-in-the-loop como atribuibilidad de responsabilidad (ejemplo: sugerencia de medicación)
  - 5. Deploy tarde (conservado)
- Slide 19 ("Lo que sí ayuda"): light edit — eliminado "datos reales después" para no contradecir el bloque 4 de las 48h.

**Cierre (slide 20)**
- Slide 20 ("Recursos adicionales"): nuevo slide. Link a futuro repo público con código de ejemplo (Python+Node call, function calling, mini-agente con loop, pattern agente redactor). Marcado como pendiente de publicar.
- Slide cierre: agregada mención a Mentorium junto a Agentman.

### Feedback de Moshe (registrado)
- *"Quita Yape y Rappi, quita años. Solo Agentman + Mentorium."*
- *"Quiero ser bastante pragmático — qué haría yo en su lugar, por qué, cómo lo aplico."*
- *"Vamos a sugerir no buscar usar datos reales debido a la limitante de tiempo."*
- *"Mi posición es C [paciente→workflow, médico→agente] pero tampoco sobrepensarlo, siempre se puede pivotar."*
- *"Workflows = la opción óptima. Agentes = overkill pero de menos complejidad técnica = ruta más rápida al MVP."*
- *"No creo que la mayoría de casos sea zona gris, pero en salud aparece seguido por la naturaleza del rubro."*
- *"Foundry — usen CLI. No se peleen con la consola."*
- *"Ejemplos de código: ABC, pero como recursos en un repo público de GitHub."*

### Pendientes para Ronda 2

- [ ] **Regla heurística original de Moshe** (cuándo cambiar approach). La regla de la hora 12 es provisional.
- [ ] **Comandos `az` verificados** con sintaxis real del CLI de Foundry.
- [ ] **Slide Foundry 13a — Agent + Tools.** Decidir si se incluyen en la tabla final o se mantienen fuera.
- [ ] **Crear repo de recursos** (`desafio-ia-bago-peru-2026-recursos`) con código de ejemplo: llamada al modelo (Python+Node), function calling, mini-agente con loop, pattern agente redactor de dummies.
- [ ] **Lo que sí ayuda (slide 19)** — revisar si queda en versión final o se fusiona/elimina.
- [ ] **Caja del agente (4 componentes)** — eliminado en Ronda 1. Decidir si vuelve o no.
- [ ] **Las 3 reglas de cierre** — revisar si reflejan correctamente los nuevos énfasis (datos dummy, HITL, etc.).

**Commit:** (pendiente al cierre de la ronda)
