---
name: skill-creator
description: >
  Creates new Antigravity agent skills following the official standard (agentskills.io).
  Activate this skill when the user asks to create, generate, or scaffold a new skill,
  or when they want to teach the agent a new capability, workflow, or set of conventions.
---

# Skill Creator — Instrucciones

Cuando el usuario pida crear una nueva skill para Antigravity, sigue este proceso completo.

---

## Paso 1: Recopilar requisitos

Antes de escribir cualquier archivo, aclara con el usuario:

1. **Propósito**: ¿Qué tarea específica debe resolver la skill?
2. **Alcance**: ¿Es una skill de **workspace** (específica de este proyecto) o **global** (todos los proyectos)?
   - Workspace → `<workspace-root>/.agent/skills/<slug>/`
   - Global → `~/.gemini/antigravity/skills/<slug>/`
3. **Tipo de skill** (ver tabla abajo):
   | Tipo | Cuándo usarla | Ejemplo |
   |------|---------------|---------|
   | **Convención** | Estándares de código, guías de estilo, reglas del equipo | code-review, naming-conventions |
   | **Workflow** | Procesos multi-paso, despliegues, CI/CD | deploy-staging, release-process |
   | **Herramienta** | Uso de herramientas externas, CLIs, APIs | docker-compose, terraform-deploy |
   | **Generador** | Scaffolding de código, plantillas, boilerplate | react-component, api-endpoint |

4. **Recursos adicionales**: ¿Necesita scripts, plantillas o archivos de ejemplo?

> Si el usuario ya proporcionó suficiente contexto, no hagas preguntas redundantes. Infiere lo que puedas y confirma solo lo ambiguo.

---

## Paso 2: Nombrar la skill

Elige un nombre en formato **slug** (kebab-case, sin espacios, sin caracteres especiales):

- ✅ `code-review`, `deploy-staging`, `react-component`
- ❌ `Code Review`, `deploy_staging`, `reactComponent`

El nombre debe ser **descriptivo y conciso** — el agente lo usa para decidir si activar la skill.

---

## Paso 3: Crear la estructura de directorios

Crea la siguiente estructura mínima:

```
<ubicación>/skills/<slug>/
├── SKILL.md          ← Requerido: definición e instrucciones
├── scripts/          ← Opcional: scripts ejecutables
├── resources/        ← Opcional: plantillas, datos, configs
└── examples/         ← Opcional: ejemplos de uso
```

### Cuándo incluir directorios opcionales

- **`scripts/`**: La skill necesita ejecutar comandos o automatizar tareas (ej: scripts de despliegue, linters personalizados).
- **`resources/`**: Hay plantillas, archivos de configuración o datos que la skill referencia.
- **`examples/`**: Ejemplos concretos mejoran la comprensión del agente sobre inputs/outputs esperados.

---

## Paso 4: Escribir el `SKILL.md`

Este es el archivo más importante. Debe seguir esta estructura exacta:

### 4.1 Frontmatter YAML (obligatorio)

```yaml
---
name: <slug-de-la-skill>
description: >
  Descripción clara de qué hace la skill y cuándo debe activarse.
  El agente usa este campo para decidir si la skill es relevante.
  Sé específico: menciona acciones, tecnologías o contextos clave.
---
```

**Reglas del frontmatter:**
- `name` (opcional pero recomendado): identificador único en kebab-case.
- `description` (requerido): debe responder "¿qué hace?" y "¿cuándo se activa?".
- La descripción debe ser lo suficientemente específica para que el agente la seleccione correctamente, pero no tan larga que sea difícil de escanear.

### 4.2 Cuerpo Markdown (instrucciones)

Después del frontmatter, escribe instrucciones claras y directas. El lenguaje debe ser imperativo y orientado a la acción.

**Estructura recomendada del cuerpo:**

```markdown
# <Nombre de la Skill> — Instrucciones

Breve descripción de lo que hace la skill (1-2 oraciones).

## Pre-requisitos
<!-- Solo si aplica: dependencias, herramientas necesarias, configuración previa -->

## Instrucciones paso a paso
1. Primer paso...
2. Segundo paso...
3. ...

## Reglas y convenciones
- Regla 1...
- Regla 2...

## Árboles de decisión
<!-- Para flujos complejos con bifurcaciones -->
- Si sucede X → haz Y
- Si sucede Z → haz W

## Ejemplos
<!-- Inputs y outputs esperados -->
### Ejemplo 1: <caso>
**Input:** ...
**Output esperado:** ...
```

### 4.3 Mejores prácticas para las instrucciones

| Práctica | Descripción |
|----------|-------------|
| **Enfoque único** | Cada skill debe resolver UNA tarea específica. Si necesitas cubrir múltiples temas, crea skills separadas. |
| **Lenguaje imperativo** | Usa "Haz X", "Verifica Y", "Ejecuta Z" en lugar de "Se debería hacer X". |
| **Ejemplos concretos** | Incluye siempre al menos un ejemplo de input/output. El agente aprende mejor con ejemplos. |
| **Árboles de decisión** | Para flujos con bifurcaciones, usa "Si X → haz Y" para evitar ambigüedad. |
| **Sin redundancia** | No repitas información del `description` del frontmatter en el cuerpo. |
| **Paths explícitos** | Si la skill referencia archivos, usa paths relativos al root de la skill. |

---

## Paso 5: Validar la skill creada

Antes de terminar, verifica:

- [ ] El archivo `SKILL.md` existe en la ubicación correcta
- [ ] El frontmatter YAML tiene al menos el campo `description`
- [ ] El frontmatter está delimitado por `---` al inicio y al final
- [ ] Las instrucciones son claras, imperativas y con ejemplos
- [ ] El nombre de la skill es un slug válido (kebab-case)
- [ ] Los directorios opcionales solo se crean si son necesarios
- [ ] Si hay scripts, tienen permisos de ejecución

---

## Plantillas rápidas

### Plantilla: Skill de Convención

```yaml
---
name: <nombre>
description: >
  Aplica las convenciones de <X> del equipo al escribir o revisar código.
  Activar cuando el usuario trabaje con <tecnología/área>.
---
```

```markdown
# <Nombre> — Convenciones

## Reglas
1. ...
2. ...

## Ejemplos

### ✅ Correcto
<código correcto>

### ❌ Incorrecto
<código incorrecto>
```

### Plantilla: Skill de Workflow

```yaml
---
name: <nombre>
description: >
  Guía el proceso de <workflow> paso a paso.
  Activar cuando el usuario necesite <acción>.
---
```

```markdown
# <Nombre> — Workflow

## Pre-requisitos
- ...

## Pasos
1. ...
2. ...

## Troubleshooting
- Si falla X → intentar Y
```

### Plantilla: Skill de Generador

```yaml
---
name: <nombre>
description: >
  Genera <artefacto> siguiendo los patrones del proyecto.
  Activar cuando el usuario pida crear un nuevo <componente/módulo/etc>.
---
```

```markdown
# <Nombre> — Generador

## Estructura generada
<tree del output>

## Convenciones del código generado
- ...

## Ejemplo de uso
**Input:** "Crea un componente Button"
**Output:** <archivos generados>
```

---

## Referencia rápida: Ubicaciones de skills

| Tipo | Path | Cuándo usar |
|------|------|-------------|
| Workspace | `<workspace>/.agent/skills/<slug>/` | Flujos específicos del proyecto o equipo |
| Global | `~/.gemini/antigravity/skills/<slug>/` | Utilidades personales, herramientas generales |
