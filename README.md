# /grill-me — Diagnosis Before Action

A Claude skill for structured decision-making through interactive surveys before taking action.

**English** • [Español](#español)

## Overview

`/grill-me` is a Claude skill that implements a three-level diagnostic survey system to clarify ambiguous requests before executing. It's designed for makers who prefer **diagnosis before action** and **step-by-step confirmation**.

Perfect for:
- Disambiguating requests with multiple interpretations
- Handling irreversible actions with explicit confirmation
- Exploring technical complexity before diving into solutions
- Building confidence in decision-making workflows

## Quick Start

### Installation

1. Copy `SKILL.md` to your Claude skills directory:
   ```
   ~/.claude/skills/grill-me/SKILL.md
   ```
   Or use Claude's Skills UI to add this skill.

2. Invoke it:
   ```
   /grill-me - Your question here
   /grill-me critical - Delete production data
   /grill-me deep - Migrate complex system
   ```

### Three Levels

| Level | Trigger | Use Case |
|-------|---------|----------|
| **`/grill-me`** | Ambiguity or trade-offs | "Build me a dashboard" → asks about scope, stack, data |
| **`/grill-me critical`** | Irreversible actions | "Delete old files" → explicit warning + confirmation |
| **`/grill-me deep`** | Technical complexity | "Migrate to Fabric" → constraints, preferences, trade-offs |

## How It Works

```
User writes request
    ↓
Claude detects ambiguity/criticality/complexity
    ↓
Diagnosis (1-2 paragraph summary)
    ↓
Interactive survey (ask_user_input_v0)
    ↓
User selects from options
    ↓
Step-by-step execution based on choice
```

### Example Flow

**Input:**
```
/grill-me - Optimize this Power BI query
```

**Claude Response:**
1. **Diagnosis:** "I see a 200K-row query taking 30 seconds to refresh. There are 3 main approaches."
2. **Survey:** Interactive buttons asking "What's your main constraint? (Refresh time / Memory / Maintainability / Flexibility)"
3. **Next:** "Once you choose, I'll show you step-by-step how to implement option X"

---

## Documentation

- **[SKILL.md](./SKILL.md)** — Complete technical spec and examples
- **[docs/levels.md](./docs/levels.md)** — Deep dive into each level
- **[docs/triggering-logic.md](./docs/triggering-logic.md)** — Auto-detection behavior
- **[examples/](./examples/)** — Real-world case studies for each level

## Features

✅ **Three diagnostic levels** — default, critical, deep  
✅ **Auto-detection** — applies appropriate level even if you don't specify  
✅ **Structured surveys** — interactive options via `ask_user_input_v0`  
✅ **Step-by-step workflow** — confirmation gates before execution  
✅ **Framework-agnostic** — works with any Claude workflow  
✅ **Bilingual** — Spanish and English documentation  

## Philosophy

This skill embodies three principles:

1. **Diagnosis before action** — Never execute without clarifying intent
2. **Step-by-step confirmation** — Confirm each decision before the next
3. **Direct challenge** — Clear options, no gentle hedging

It's built for makers who think deeply before shipping.

---

## Usage Examples

### Example 1: Default Level (Ambiguity)
```
User: "/grill-me - Make me a dashboard"

Claude:
Diagnosis: You could mean MVP or full analytics suite. 
Stack matters too (Power BI vs. Tableau vs. custom).

Survey: 
- Scope: MVP / Comprehensive / Custom
- Stack: Power BI / Tableau / Looker / Custom
- Data: Mock / Real-time / Hybrid
```

### Example 2: Critical Level (Irreversible)
```
User: "/grill-me critical - Delete draft-2023"

Claude:
⚠️ PERMANENT ACTION DETECTED

Diagnosis: This will remove "draft-2023" permanently. 
No undo available. 5 other files reference this.

Survey:
- Confirm deletion: YES / NO / Review first / Archive instead
```

### Example 3: Deep Level (Technical)
```
User: "/grill-me deep - Migrate RFM model to v3"

Claude:
Diagnosis: 500MB model, 15 measures, 20 dependent reports.
Decisions needed on: partitioning, compression, refresh strategy.

Survey:
- Priority: Speed / Storage / Query Performance / Balanced
- Future volume: <1GB / 1-5GB / >5GB
- Budget: Unlimited / Limited / Premium-only
```

---

## When to Use / When NOT to Use

### ✅ Use /grill-me when:
- Request has 2+ valid interpretations
- Trade-offs exist (speed vs. cost, simplicity vs. power)
- Action is irreversible (delete, publish, commit)
- Complex technical decision with constraints

### ❌ Don't use when:
- Request is already clear and specific
- Continuation of previous decision ("go ahead")
- Pure information request ("What is DAX syntax?")
- Single obvious path forward

---

## For Teams

This skill works great in team contexts where:
- You want to prevent miscommunication before it starts
- You need explicit confirmation on critical actions
- Technical decisions benefit from structured exploration
- Multiple interpretations could lead to rework

---

## Versions

**v1.0** (Sept 2026)
- Initial release
- Three levels: default, critical, deep
- Auto-detection logic
- Full documentation in English & Spanish

---

## Contributing

Have ideas for improvement?

1. Test the skill in your workflows
2. Document edge cases or new use patterns
3. Submit issues or PRs with examples

---

## License

MIT License — Use freely in personal and commercial projects. See [LICENSE](./LICENSE) for details.

---

## Questions?

See [SKILL.md](./SKILL.md) for technical details, or check [examples/](./examples/) for real workflows.

---

---

# Español

## Descripción

`/grill-me` es un skill de Claude que implementa un sistema de surveys diagnósticos en tres niveles para aclarar solicitudes ambiguas antes de ejecutar. Diseñado para makers que prefieren **diagnóstico antes de acción** y **confirmación paso a paso**.

Perfecto para:
- Desambiguar solicitudes con múltiples interpretaciones
- Manejar acciones irreversibles con confirmación explícita
- Explorar complejidad técnica antes de lanzarse a soluciones
- Construir confianza en workflows de toma de decisiones

## Inicio Rápido

### Instalación

1. Copia `SKILL.md` a tu directorio de skills de Claude:
   ```
   ~/.claude/skills/grill-me/SKILL.md
   ```
   O usa la UI de Skills de Claude para agregar este skill.

2. Invócalo:
   ```
   /grill-me - Tu pregunta aquí
   /grill-me critical - Borrar datos de producción
   /grill-me deep - Migrar sistema complejo
   ```

## Tres Niveles

| Nivel | Trigger | Caso de Uso |
|-------|---------|-----------|
| **`/grill-me`** | Ambigüedad o trade-offs | "Hazme un dashboard" → pregunta scope, stack, datos |
| **`/grill-me critical`** | Acciones irreversibles | "Borra archivos viejos" → advertencia explícita + confirmación |
| **`/grill-me deep`** | Complejidad técnica | "Migra a Fabric" → constraints, preferencias, trade-offs |

## Documentación

- **[SKILL.md](./SKILL.md)** — Especificación técnica completa y ejemplos
- **[docs/levels.md](./docs/levels.md)** — Análisis profundo de cada nivel
- **[docs/triggering-logic.md](./docs/triggering-logic.md)** — Comportamiento de auto-detección
- **[examples/](./examples/)** — Casos de estudio reales para cada nivel

## Filosofía

Este skill encarna tres principios:

1. **Diagnóstico antes de acción** — Nunca ejecutar sin aclarar intención
2. **Confirmación paso a paso** — Confirmar cada decisión antes de la siguiente
3. **Desafío directo** — Opciones claras, sin ambigüedades suaves

Está construido para makers que piensan profundamente antes de hacer ship.

## Licencia

MIT License — Úsalo libremente en proyectos personales y comerciales. Ver [LICENSE](./LICENSE) para detalles.

---

**Made with ❤️ for thoughtful decision-making**
