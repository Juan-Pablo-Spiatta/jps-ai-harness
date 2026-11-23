# Adaptador de agentes

Cómo convertir cada rol definido en `.agents/roles/` en un agente/subagente nativo de cada herramienta, sin duplicar la metodología ni el comportamiento del rol.

## Documentación oficial

**Fuentes consultadas el:** `2026-11-20`

Todo lo que se indica abajo sobre formatos de herramienta sale de estas páginas; si una herramienta cambia su formato, manda su documentación sobre este archivo. Actualiza la fecha anterior solo tras reconsultar de verdad las URLs (y ajustar este archivo si hubo cambios).

| Herramienta | Documentación oficial |
| --- | --- |
| GitHub Copilot en VS Code | [Custom agents in VS Code](https://code.visualstudio.com/docs/agent-customization/custom-agents) · [Custom agent file reference](https://code.visualstudio.com/docs/agents/reference/custom-agent-file-reference) |
| Claude Code | [Create custom subagents](https://code.claude.com/docs/en/sub-agents) |
| Cursor | [Subagents](https://cursor.com/docs/subagents) |
| Codex | [Subagents](https://developers.openai.com/codex/subagents) |

### Frescura antes de generar adaptadores nativos

Aplica cuando el humano pide crear, regenerar o publicar los subagentes nativos para una o más herramientas.

1. Lee la fecha de **Fuentes consultadas el** (arriba) y calcúlala frente a la fecha de hoy.
2. **Si han pasado 30 días o menos:** genera con las plantillas y la tabla de roles de este archivo.
3. **Si han pasado más de 30 días:**
   - Avisa al humano que este espejo de formatos puede estar desactualizado (fecha de consulta + días transcurridos).
   - Ofrece: **(A)** reconsultar las URLs oficiales de la herramienta pedida, actualizar este archivo (campos, plantillas y la fecha) si hay diferencias, y luego generar; **(B)** continuar igual con el contenido actual bajo riesgo.
   - Si el humano insiste en **(B)**, genera los adaptadores nativos con lo que hay aquí, sin afirmar que el formato sigue vigente. Deja constancia breve en la respuesta de que se generó sin revalidar la documentación oficial.
4. No inventes campos ni carpetas que no estén en este archivo ni en la documentación oficial reconsultada. No copies procedimiento SDD ni el contenido de los roles en los adaptadores nativos.

## Principio

- **Fuente única de verdad del comportamiento:** `.agents/roles/<subagente>.md`. Ciclo, gates y tabla de subagentes: `constitution.md`. Reglas de conducta del agente: `AGENTS.md`.
- **Adaptadores finos:** el archivo de cada herramienta solo aporta lo que esa herramienta necesita para descubrir el agente (`name`, `description`, herramientas, modelo) y le ordena leer y seguir el rol. **No** copiar procedimiento, brief/return, rutas SDD ni reglas de fase en el adaptador.
- Ninguna de las cuatro documentaciones describe un mecanismo para importar otro archivo dentro de la definición del agente; por eso la instrucción de leer el rol va en el cuerpo y el agente necesita herramientas de lectura.
- **Nombres:** el archivo de rol y las rutas bajo `sdd/progress/` usan `snake_case` (`spec_author`). El `name` del agente nativo usa **kebab-case** (`spec-author`) y debe ser el mismo en las cuatro herramientas. La ruta del rol en el cuerpo del adaptador sigue siendo `.agents/roles/spec_author.md`.

## Roles vigentes → metadatos del adaptador

Tomados de `constitution.md` (sección 3) y de `.agents/roles/`. Usar estos valores al crear o actualizar adaptadores; no inventar roles fuera de esta tabla.

| Rol (archivo) | `name` (agente) | `description` (cuándo usarlo) | Herramientas orientativas |
| --- | --- | --- | --- |
| `leader.md` | `leader` | Orquesta el ciclo SDD: decide la fase, escribe briefs, delega en subagentes, controla gates humanos y mantiene `sdd/progress/`. Úsalo al empezar o retomar una US o el ciclo. | Lectura + edición de progreso + capacidad de invocar otros agentes (`agent` en Copilot; heredar herramientas de delegación en el resto). |
| `spec_author.md` | `spec-author` | Redacta spec, plan o tasks (una fase por encargo) bajo `sdd/specs/<NNNN-feature-slug>/` a partir del brief. Úsalo en las fases Spec, Plan o Tasks. | Lectura, búsqueda y edición (escribe artefactos y `return.md`). |
| `implementer.md` | `implementer` | Ejecuta las tasks aprobadas. Úsalo en la fase Implement. | Lectura, búsqueda, edición y ejecución (código + verificación). |
| `reviewer.md` | `reviewer` | Revisa la implementación contra spec, plan, tasks y constitution; emite el informe. Úsalo en la fase Review. | Lectura, búsqueda y edición (solo el informe / `return.md`). |
| `explorer.md` | `explorer` | Recopila información verificable a demanda. Úsalo cuando haga falta investigar el repo sin modificar artefactos de fase. | Solo lectura y búsqueda. En Cursor: `readonly: true`. |

El cuerpo del adaptador es siempre el mismo patrón (cambiar solo la ruta del rol):

```text
Antes de hacer nada, lee `AGENTS.md` y `.agents/roles/<subagente>.md`.
Sigue ese rol al completo (incluye lo que el rol pide leer, p. ej. constitution.md y el brief).
Si este archivo y el rol se contradicen, manda el rol.
```

Precedencia (no la redefine este archivo): `AGENTS.md` y `constitution.md` mandan sobre el rol; el rol manda sobre el adaptador.

## Resumen de carpetas por herramienta

| Herramienta | Carpeta (proyecto) | Archivo | Formato | Campos obligatorios |
| --- | --- | --- | --- | --- |
| Copilot (VS Code) | `.github/agents/` | `<nombre>.agent.md` | Markdown + frontmatter YAML | `description` (requerido por el schema de Copilot) |
| Claude Code | `.claude/agents/` | `<nombre>.md` | Markdown + frontmatter YAML | `name`, `description` |
| Cursor | `.cursor/agents/` | `<nombre>.md` | Markdown + frontmatter YAML | Ninguno (`name` se deriva del archivo) |
| Codex | `.codex/agents/` | `<nombre>.toml` | TOML | `name`, `description`, `developer_instructions` |

---

## 1. GitHub Copilot en VS Code

**Carpeta:** `.github/agents/` (workspace). Acepta archivos `.agent.md` o `.md`. A nivel usuario: `~/.copilot/agents/`.

**Campos útiles** (según la *Custom agent file reference*):

- `name`: nombre en la UI; por defecto, el nombre del archivo.
- `description`: qué hace y cuándo usarlo. Lo exige el schema de Copilot.
- `tools`: en el harness Copilot admite los alias `execute`, `read`, `edit`, `search`, `agent`, `web`, `todo`, o `*`.
- `model`, `user-invocable` (si aparece en el desplegable), `disable-model-invocation` (si otros agentes pueden invocarlo como subagente).

**Plantilla** — `.github/agents/spec-author.agent.md` (ejemplo; repetir por cada fila de la tabla de roles):

```markdown
---
name: spec-author
description: Redacta spec, plan o tasks (una fase por encargo) bajo sdd/specs/. Úsalo en las fases Spec, Plan o Tasks.
tools: ['read', 'search', 'edit']
---
Antes de hacer nada, lee `AGENTS.md` y `.agents/roles/spec_author.md`.
Sigue ese rol al completo (incluye lo que el rol pide leer, p. ej. constitution.md y el brief).
Si este archivo y el rol se contradicen, manda el rol.
```

**Uso:** selecciónalo en el desplegable **Agent** del chat, o deja que otro agente lo invoque como subagente.

**Notas:**

- Las `handoffs` solo funcionan en el harness **Local**, que está deprecado (se retira en febrero de 2027).
- VS Code también lee `.claude/agents/` (formato Claude). Si tienes el mismo agente en `.github/agents/` y en `.claude/agents/`, revisa en el editor **Chat: Open Customizations** que no aparezca duplicado.
- Para `leader`, incluye el alias `agent` entre las herramientas para poder delegar.

---

## 2. Claude Code

**Carpeta:** `.claude/agents/` (proyecto). A nivel usuario: `~/.claude/agents/`. Se escanean de forma recursiva, así que se pueden usar subcarpetas; la identidad del agente sale solo de `name`.

**Campos** (según *Frontmatter reference*):

- Obligatorios: `name` (sin `:`) y `description` (Claude la usa para decidir cuándo delegar).
- Opcionales: `tools` (si se omite, hereda todas), `disallowedTools`, `model` (`sonnet`, `opus`, `haiku`, ID completo o `inherit`), `permissionMode`, `skills`, `maxTurns`, entre otros.
- Los nombres de campo son camelCase exactos; un campo mal escrito se ignora sin error.

**Plantilla** — `.claude/agents/spec-author.md`:

```markdown
---
name: spec-author
description: Redacta spec, plan o tasks (una fase por encargo) bajo sdd/specs/. Úsalo en las fases Spec, Plan o Tasks.
tools: Read, Grep, Glob, Write, Edit
---
Antes de hacer nada, lee `AGENTS.md` y `.agents/roles/spec_author.md`.
Sigue ese rol al completo (incluye lo que el rol pide leer, p. ej. constitution.md y el brief).
Si este archivo y el rol se contradicen, manda el rol.
```

**Uso:** delegación automática por `description`, o explícita: "Use the spec-author agent to …".

**Notas:**

- El cuerpo se convierte en el system prompt del subagente. Los subagentes personalizados cargan `CLAUDE.md`, salvo que se use `omitClaudeMd`. La documentación no dice que lean `AGENTS.md` por sí solos; por eso la plantilla lo pide de forma explícita.
- Claude Code detecta cambios en `.claude/agents/` en unos segundos. Si no encuentra el agente, reinicia la sesión.
- Para `explorer`, restringe herramientas a lectura/búsqueda (p. ej. sin `Write`/`Edit`), alineado con los límites del rol.

---

## 3. Cursor

**Carpeta:** `.cursor/agents/` (proyecto). A nivel usuario: `~/.cursor/agents/`.

**Campos** (todos opcionales):

- `name`: por defecto, el nombre del archivo. Minúsculas y guiones.
- `description`: el agente la lee para decidir si delega.
- `model`: `inherit` (por defecto) o un ID de modelo.
- `readonly`: si es `true`, no puede editar archivos.
- `is_background`: si es `true`, no bloquea al agente padre.

**Plantilla** — `.cursor/agents/spec-author.md`:

```markdown
---
name: spec-author
description: Redacta spec, plan o tasks (una fase por encargo) bajo sdd/specs/. Úsalo en las fases Spec, Plan o Tasks.
model: inherit
readonly: false
---
Antes de hacer nada, lee `AGENTS.md` y `.agents/roles/spec_author.md`.
Sigue ese rol al completo (incluye lo que el rol pide leer, p. ej. constitution.md y el brief).
Si este archivo y el rol se contradicen, manda el rol.
```

**Uso:** `/spec-author <tarea>` o en lenguaje natural ("Use the spec-author subagent to …").

**Notas:**

- Cursor también lee `.claude/agents/` y `.codex/agents/` por compatibilidad. Si hay nombres repetidos, `.cursor/` tiene prioridad sobre `.claude/` y `.codex/`. Si el contenido es equivalente, puedes omitir `.cursor/agents/` y dejar que Cursor use `.claude/agents/`.
- Los subagentes empiezan con el contexto vacío. El agente padre solo les pasa lo que incluye en el prompt, así que la lectura explícita del rol es necesaria.
- Para `explorer`, usa `readonly: true`.

---

## 4. Codex

**Carpeta:** `.codex/agents/` (proyecto). A nivel usuario: `~/.codex/agents/`. Un archivo TOML por agente.

**Campos:**

- Obligatorios: `name` (es la fuente de verdad, no el nombre del archivo), `description` y `developer_instructions`.
- Opcionales: `model`, `model_reasoning_effort`, `model_reasoning_summary`, `model_verbosity`, y `features.*` para desactivar capacidades.
- `sandbox_mode`, `approval_policy` y `mcp_servers` **no** sobrescriben la configuración del padre. Las instrucciones pueden pedir "no edites", pero eso no crea un sandbox de solo lectura.
- Los ajustes globales van en `[agents]` dentro de `.codex/config.toml` (p. ej. `max_concurrent_threads_per_session`).

**Plantilla** — `.codex/agents/spec-author.toml`:

```toml
name = "spec-author"
description = "Redacta spec, plan o tasks (una fase por encargo) bajo sdd/specs/. Úsalo en las fases Spec, Plan o Tasks."
developer_instructions = """
Antes de hacer nada, lee `AGENTS.md` y `.agents/roles/spec_author.md`.
Sigue ese rol al completo (incluye lo que el rol pide leer, p. ej. constitution.md y el brief).
Si este archivo y el rol se contradicen, manda el rol.
"""
```

**Uso:** Codex delega cuando se le pide de forma directa ("spawn the spec-author agent to …") o cuando lo indica un `AGENTS.md` o una skill aplicable.

**Notas:**

- Los ejemplos oficiales usan `snake_case` en `name` (p. ej. `pr_explorer`). La documentación no indica que kebab-case esté prohibido, pero tampoco lo muestra: **no verificado**. Si falla, usa el `snake_case` del archivo de rol (`spec_author`) de forma consistente en las cuatro herramientas.
- Los subagentes heredan el sandbox y los permisos de la sesión padre.

---

## Cómo publicar o añadir un rol

1. Define el subagente en `constitution.md` (sección 3) si es parte de la metodología.
2. Crea o completa `.agents/roles/<subagente>.md` con el comportamiento completo (única fuente de verdad del rol).
3. Añade una fila a la tabla [Roles vigentes → metadatos del adaptador](#roles-vigentes--metadatos-del-adaptador): `name` en kebab-case y `description` que diga **cuándo** usarlo (alineada al propósito del rol).
4. Antes de crear archivos nativos, aplica [Frescura antes de generar adaptadores nativos](#frescura-antes-de-generar-adaptadores-nativos) (umbral 30 días; aviso y continuar solo si el humano insiste).
5. Crea un adaptador por herramienta con las plantillas de arriba. Cambia solo `name`, `description`, la ruta del rol y las herramientas o el modelo. No copies el contenido del rol.
6. Verifica en cada herramienta que el agente aparece y que lee el rol: pídele una tarea pequeña y revisa en su actividad que haya abierto `.agents/roles/<subagente>.md`.
7. No registres cada rol como fila del glosario de `AGENTS.md`. El glosario apunta a `.agents/roles/` y a este adaptador; la lista de subagentes vive en `constitution.md`.
