---
name: grill-me
description: Encuestas interactivas para diagnosis antes de acción. Invocá con /grill-me [nivel], donde nivel es opcional. Soporta 3 modos — /grill-me (ambigüedad/trade-offs), /grill-me critical (decisiones irreversibles con advertencias), /grill-me deep (cuestiones técnicas complejas). Pide confirmación estructurada antes de actuar. Alineado con preferencia de diagnóstico antes de ejecución y step-by-step workflow.
---

# /grill-me — Diagnosis Before Action

## Propósito

Encuestas interactivas que desambiguan tu solicitud antes que Claude tome decisiones. Alineado con preferencia de diagnóstico antes de ejecución y confirmación paso a paso.

---

## Niveles de Activación

El skill soporta 3 niveles opcionales:

### 1. `/grill-me` (default)
**Cuándo:** Hay ambigüedad moderada o múltiples interpretaciones válidas

- La solicitud podría entenderse de 2+ formas
- Hay trade-offs claros entre opciones (velocidad vs. robustez, costo vs. cobertura)
- Decisiones que afectan dirección general o arquitectura
- Necesidad de confirmar scope, prioridades o constraints antes de avanzar

**Qué pasa:** Encuesta 1-3 preguntas de clarificación. Espero tu respuesta antes de actuar.

**Ejemplo:**
```
User: "Hazme un dashboard"
→ /grill-me:
  ¿Scope?
  - MVP rápido (2-3 KPIs)
  - Completo (10+ métricas)
  
  ¿Stack preferido?
  - Power BI
  - Tableau
  - Herramienta custom
```

---

### 2. `/grill-me critical`
**Cuándo:** Decisiones irreversibles o de alto riesgo

- Acciones que no se pueden deshacer (borrar, enviar, publicar)
- Cambios en configuración de seguridad o credenciales
- Modificaciones en datos críticos o productivos
- Compromisos financieros o contractuales
- Cambios en sistemas que afecten a otros usuarios/stakeholders

**Qué pasa:** Encuesta detallada + resumen de consecuencias. Pido confirmación explícita (SÍ/NO/Alternativa).

**Ejemplo:**
```
User: "/grill-me critical - Borra los drafts antiguos"

⚠️ ACCIÓN PERMANENTE DETECTADA

Diagnosis:
Esto eliminará archivos de forma permanente. No hay undo.

[Encuesta]
¿Confirmás?
- SÍ, borrar ahora
- NO, mantener
- Ver qué contiene primero
```

---

### 3. `/grill-me deep`
**Cuándo:** Cuestiones técnicas específicas o análisis profundo

- Arquitecturas complejas con múltiples trade-offs técnicos
- Decisiones que requieren expertise en dominios específicos
- Migraciones, refactors, o cambios sistémicos
- Problemas de performance/escalabilidad con varias aproximaciones posibles
- Cuando necesito entender constraints antes de proponer solución

**Qué pasa:** Encuesta 2-4 preguntas técnicas sobre constraints, preferencias de stack, limitaciones de tiempo/recurso, etc.

**Ejemplo:**
```
User: "/grill-me deep - Migra el modelo v2 a v3"

Diagnosis:
Veo un modelo RFM de 500MB con 15 medidas. Hay decisiones en particionamiento, 
compresión, y refresh strategy.

[Encuesta]
¿Cuál es tu prioridad?
- Minimizar refresh time
- Minimizar storage
- Maximizar query performance
- Balanceado

¿Volumen esperado a futuro?
- <1GB (actual)
- 1-5GB
- >5GB

¿Constraints de licencia?
- Ilimitado
- Budget limitado (especificar)
- Premium solo para producción
```

---

## Cómo Funciona Internamente

Todos los niveles usan la herramienta `ask_user_input_v0` que renderiza encuestas con tarjetas clickeables.

### Estructura de Respuesta

**Entrada del usuario:**
```
/grill-me critical
Quiero publicar esto en producción mañana
```

**Mi respuesta (siempre 3 partes):**

1. **Diagnosis** — Qué vi en tu solicitud (resumen en prosa)
2. **Encuesta** — ask_user_input_v0 con 2-4 opciones clickeables
3. **Siguiente paso** — Cómo procedo una vez respondas (step-by-step execution)

---

## Tabla Comparativa de Niveles

| Aspecto | `/grill-me` | `/grill-me critical` | `/grill-me deep` |
|---------|-------------|----------------------|------------------|
| **Trigger** | Ambigüedad moderada | Acciones irreversibles | Problemas técnicos complejos |
| **Preguntas** | 1-3 | 2-4 + resumen | 2-4 técnicas |
| **Tono** | Neutral, directo | Formal, con ⚠️ | Técnico, exploratorio |
| **Confirmación** | Implícita en opciones | Explícita (SÍ/NO) | Por cada decisión mayor |
| **Ejemplo** | "¿Scope?" | "Esto es PERMANENTE. ¿Seguro?" | "¿Constraints de performance?" |

---

## Flujo de Decisión

```
Usuario escribe solicitud
         ↓
¿Está clara y es específica?
    NO → Claude decide qué nivel aplicar:
         ├─ ¿Hay trade-offs o ambigüedad? → /grill-me
         ├─ ¿Decisión irreversible? → /grill-me critical
         ├─ ¿Problema técnico complejo? → /grill-me deep
         │
    SÍ → Procede directo (diagnóstico rápido, sin encuesta)
         ↓
    Diagnosis + Encuesta (ask_user_input_v0)
         ↓
    Espera respuesta del usuario
         ↓
    Step-by-step execution basado en respuesta
```

---

## Uso Manual vs. Auto-Trigger

### Opción A: User especifica nivel explícitamente
```
/grill-me critical - Borra esto
/grill-me deep - Migra el modelo
/grill-me - Optimize este query
```
→ Claude respeta el parámetro exacto

### Opción B: User NO especifica (solo `/grill-me`)
```
/grill-me - Hazme un dashboard
```
→ Claude auto-detecta: "Hay múltiples formas de interpretar esto" → aplica `/grill-me` default

### Opción C: User no dice nada (aplicación automática)
```
Borra el archivo importante
```
→ Claude auto-detecta: "Decisión irreversible" → automáticamente aplica `/grill-me critical` sin que usuario lo pida

---

## Cuándo NO Invocar /grill-me

- ✗ La solicitud ya es clara y específica
- ✗ Ya confirmaste pasos anteriores en la misma sesión (continuación obvia)
- ✗ Es una pregunta puramente informativa ("¿Cuál es la sintaxis de DAX?")
- ✗ User dice "dale, adelante" (continuación de decisión anterior)

## Cuándo SÍ Invocar

- ✓ Hay 2+ interpretaciones válidas
- ✓ Trade-offs técnicos o de producto
- ✓ Acción irreversible
- ✓ Problema complejo que necesita información de constraints

---

## Múltiples Decisiones en Una Solicitud

Si es una gran tarea con varias decisiones:

```
/grill-me deep
Necesito:
1. Migrar datos de SQL a Fabric
2. Refactorizar modelo RFM
3. Actualizar 5 reports conectados
```

→ **1 encuesta que cubre TODAS las decisiones**, no 3 encuestas separadas. Ejemplo:

```
[Encuesta única]
¿Migración de datos: enfoque?
- Full load + incremental refresh
- Staging table + particionamiento
- Direct query (si volumen lo permite)

¿Prioridad del refactor?
- Completa (best practices, optimización)
- Mínima (solo lo necesario para Fabric)

¿Timeline?
- ASAP (esta semana)
- 2 semanas
- 1 mes (planificado)
```

---

## Parámetros Resumidos

```
/grill-me                    → Diagnosis + encuesta (default, ambigüedad/trade-offs)
/grill-me critical           → Irreversibles, con advertencias explícitas
/grill-me deep               → Técnicas específicas/complejas, constraints-heavy
```

**Nota:** Parámetros son case-insensitive: `/grill-me CRITICAL` = `/grill-me critical` = `/grill-me Critical`

---

## Integración con Workflow Existente

Percy tiene `grill-me: true` en preferencias. Este skill refuerza:
- ✓ **Diagnosis before action** — nunca salto al código sin desambiguar
- ✓ **Step-by-step confirmation** — encuestas antes de cada decisión mayor
- ✓ **Direct challenge over gentle framing** — tono directo, opciones claras

---

## Ejemplos Detallados

### Ejemplo 1: Default (Trade-off moderado)
```
User: "/grill-me - Quiero optimizar este query de Power BI"

Diagnosis:
Veo un query con 200K registros que tarda 30 segundos en refresh. 
Hay 3 enfoques principales con diferentes trade-offs.

[Encuesta]
¿Cuál es tu constrainte mayor?
- Refresh time (query duration)
- Memory usage en el modelo
- Complejidad de mantenimiento
- Puedo cambiar la arquitectura
```

### Ejemplo 2: Critical (Irreversible)
```
User: "/grill-me critical - Borra todos los drafts del 2024"

⚠️ ACCIÓN PERMANENTE DETECTADA

Diagnosis:
Esto eliminará X archivos de forma permanente. No hay papelera de reciclaje.
Afectará a Y usuarios que tengan referencias a estos drafts.

[Encuesta]
¿Confirmás la eliminación?
- SÍ, borrar ahora
- NO, mantener
- Quiero ver la lista primero
- Archivar en lugar de borrar (alternativa)
```

### Ejemplo 3: Deep (Técnico complejo)
```
User: "/grill-me deep - Migra el modelo RFM a la v3 architecture"

Diagnosis:
Veo un modelo RFM de 500MB con 15 medidas, usado por 20 reports.
Hay decisiones en: particionamiento de datos, compresión, refresh strategy,
y backward compatibility con reports antiguos.

[Encuesta]
¿Cuál es tu prioridad?
- Minimizar refresh time
- Minimizar storage
- Maximizar query performance
- Balanceado (bueno en todo)

¿Volumen esperado a futuro?
- <1GB (actual)
- 1-5GB
- >5GB

¿Constraints de licencias/budget?
- Ilimitado
- Budget limitado
- Premium solo para reportes críticos

¿Backward compatibility?
- Crítica (reports antiguos deben funcionar igual)
- Can refactor reports junto con modelo
- No matter (estamos listos para romper cosas)
```

---

## Technical Implementation

### Internamente, Claude:

1. Parsea el `/grill-me [parámetro]`
2. Lee la solicitud para detectar ambigüedad/irreversibilidad/complejidad técnica
3. Genera diagnosis (1-2 párrafos)
4. Invoca `ask_user_input_v0` con estructura apropiada
5. Espera respuesta con `questions` estructura
6. Procede según respuesta con step-by-step confirmation

### ask_user_input_v0 schema:
```json
{
  "questions": [
    {
      "question": "Tu pregunta aquí",
      "options": ["Opción A", "Opción B", "Opción C"],
      "type": "single_select"  // o multi_select, rank_priorities
    }
  ]
}
```

---

## Changelog / Versions

**v1.0** (Sept 2026)
- Inicial: 3 niveles (default, critical, deep)
- Auto-detection logic
- Integración con ask_user_input_v0
- Alineación con preferencias existentes (grill-me: true, step-by-step, direct challenge)

