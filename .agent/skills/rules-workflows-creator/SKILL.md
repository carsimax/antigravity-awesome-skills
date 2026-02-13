---
name: rules-workflows-creator
description: >
  Genera Project Rules y Workflows de Antigravity siguiendo los estándares oficiales.
  Activa esta skill cuando el usuario pida crear reglas de proyecto, convenciones,
  o workflows de automatización (slash commands).
---

# Rules & Workflows Creator — Instrucciones

Esta skill guía la creación de **Project Rules** (contexto) y **Workflows** (pasos) para el agente Antigravity.

---

## Paso 1: Definir el artefacto

Determina con el usuario qué necesita crear:

| Tipo | Propósito | ubicación Recomendada |
|------|-----------|------------------------|
| **Rule** | Reglas, convenciones o guías de estilo "Always On" o activadas por archivos. | `.agent/rules/*.md` |
| **Workflow** | Secuencias de pasos repetitivos invocables mediante `/comando`. | `.agent/workflows/*.md` |

---

## Paso 2: Configurar Rules

Si es una **Rule**, define cómo se activará:

1. **Always On**: Se aplica siempre en el workspace. No requiere frontmatter especial (o usa `alwaysApply: true`).
2. **Model Decision**: El modelo decide si usarla basa en una descripción. Requiere YAML frontmatter con `description`.
3. **Manual**: El usuario la invoca con `@rule-name`. Requiere YAML frontmatter con `description`.
4. **Glob**: Se aplica solo a archivos que coincidan con un patrón (ej: `src/**/*.ts`). Requiere YAML frontmatter con `globs`.

### Formato de Rule (.md)
```yaml
---
description: >
  Explica aquí cuándo debe activarse esta regla.
  Ej: "Aplica cuando se editan componentes React".
globs:
  - "**/*.tsx"
  - "**/*.ts"
---

# Título de la Regla

Contenido de la regla en Markdown...
```

---

## Paso 3: Configurar Workflows

Si es un **Workflow**, define el comando `/`.

### Formato de Workflow (.md)
```yaml
---
description: >
  Descripción clara de qué hace el workflow.
  Ej: "Despliega la aplicación a producción".
---

# [Título del Workflow]

1. Primer paso...
// turbo
2. Comando que se puede auto-ejecutar...
3. Call /otro-workflow (Composición)
```

---

## Paso 4: Mejores Prácticas

- **Límite**: Máximo 12,000 caracteres por archivo.
- **@Mentions**: Usa `@/path/to/file` para referenciar otros archivos dentro de las reglas.
- **Lenguaje**: Usa lenguaje imperativo y directo ("Haz X", "Verifica Y").
- **Turbo**: Usa `// turbo` sobre comandos de terminal en workflows para permitir auto-ejecución.

---

## Recursos y Ejemplos

- [Plantillas de Rules y Workflows](resources/rules-templates.md)
- [Ejemplos de Rules](examples/example-rules.md)
- [Ejemplos de Workflows](examples/example-workflows.md)
