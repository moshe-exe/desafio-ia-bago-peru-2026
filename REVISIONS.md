# Revisiones — desafio-ia-bago-peru-2026

**Estado:** `review-2`
**Rondas completadas:** 2
**Mínimo para aprobar:** 2
**Última actualización:** 2026-06-03

> Cumple el mínimo de rondas. **Aprobable** mediante `/slides approve desafio-ia-bago-peru-2026` cuando Moshe confirme.

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

**Commit:** `0cc5c2d`

---

## Ronda 2 — 2026-06-03

**Foco:** reducir el deck de 24 → 18 slides para encajar mejor en los 30 min de charla (target ~1.5-2 min por slide). Pasada de consolidación, no de cambio de contenido.

### Cambios aplicados

**A) Cortes de dividers de sección (-3 slides)**
- Cortados los 3 slides "Parte 1 / Parte 2 / Parte 3" (eran `layout: section`).
- En su reemplazo: cada slide dentro de su parte lleva un **badge `abs-tr`** sutil (esquina superior-derecha, opacidad 40%, fuente mono) con el texto `Parte N · <nombre>`. El mapa del talk (slide 5) sigue cumpliendo la función de índice.

**B) Fusiones (-1 slide neta)**
- **Slide 8 "Cuándo cambiar de rumbo"** — fusión de los antiguos slides 9 (Regla heurística hora 12) + 10 (Pivotar). Estructura: dos checkpoints con dos reglas (hora 12 → recorta, hora 24 → pivota), cierre con la frase de "enamórate del problema, no de la solución".
- **Slide 16 "Top errores · y cómo evitarlos"** — fusión de los antiguos slides 20 (Top 5 errores) + 21 (Lo que sí ayuda). Tabla de 2 columnas: error → cómo evitarlo. El resto de "lo que sí ayuda" (trunk-based dev, video backup, ensayar pitch) queda como pie de slide en una línea pequeña.
- **NO fusionados:** Stack mínimo (10) + Foundry (11). Moshe vetó la fusión — dos tablas en un slide es demasiado.

**C) Cortes opcionales — todos rechazados**
- Mantenidos: Slide 9 (Hardcode estratégico), Slide 12 (Foundry — CLI > Consola). Moshe los considera valiosos.

**D) Consolidación de cierre (-1 slide)**
- Antes: 22 (Recursos adicionales) + 23 (3 reglas) + 24 (Gracias) = 3 slides.
- Después: 17 (3 reglas) + 18 (Gracias con link al repo de recursos embebido). El bloque de recursos vive ahora dentro del Gracias.

**Otros cambios**
- **Slide 4 ("El objetivo"):** removida la frase prominente "Container local + API key de IA = mockup competente". Quedó solo "**Mockup competente en 48 horas.**" + "Lo demás es criterio." (Moshe consideró que el framing era demasiado específico para el headline).

### Estructura final (18 slides)

```
1.  Title
2.  Quién soy
3.  Qué les voy a contar
4.  El objetivo
5.  Mapa del talk
[Parte 1 · El método]
6.  La regla #1: recorta hasta que duela
7.  Las 48 horas en 4 bloques
8.  Cuándo cambiar de rumbo
9.  Hardcode estratégico
[Parte 2 · La arquitectura]
10. Stack mínimo · mockup en 48h
11. Foundry — lo mínimo para 48h
12. Foundry — CLI > Consola
13. Agente vs Workflow · cómo se ve cada mockup
14. No es blanco o negro
15. El insight contraintuitivo
[Parte 3 · Los errores]
16. Top errores · y cómo evitarlos
[Cierre]
17. Las 3 reglas que te van a salvar
18. Gracias + recursos
```

### Feedback de Moshe (registrado)
- *"Tenemos muchos slides, 24 para una reunión de 30 minutos. Lo saludable es 16-18."*
- *"A) sí, recortar pero incluir algo que haga referencia a las 'partes' dentro de los slides que corresponden a cada parte."*
- *"B) 9+10 definitivamente, 13+14 no, dos tablas en un solo slide es mucho."*
- *"C) mantengamos 11 y 15, ayudame a encontrar la forma de combinar 20 y 21."*
- *"D) consolidar."*
- *"GO a todo, excepto la creación del repo de recursos que lo haremos después juntos."*
- *"El objetivo (container + API key) → quitar lo de container y api key del titulo."*

### Pendientes para Ronda 3 (si la hubiera) o pulido post-aprobación

- [ ] **Crear repo de recursos** (`desafio-ia-bago-peru-2026-recursos`) — Moshe lo hará junto con Claude después. El link ya está en slide 18 marcado como "disponible al cierre".
- [ ] **Comandos `az` verificados** con la sintaxis real del CLI de Foundry (slide 12 los usa de forma indicativa).
- [ ] **Slide Foundry 11 — Agent + Tools** — decidir si vuelven a la tabla o se mantienen fuera.
- [ ] **Las 3 reglas de cierre (slide 17)** — confirmar que reflejan los énfasis nuevos de Ronda 1 (dummies, HITL, etc.) o re-craft.
- [ ] **Verificar tiempo real de la charla** — leerla en voz alta una vez antes de aprobar para confirmar que 18 slides caben en 30 min.

**Commit:** `646f7bc`
