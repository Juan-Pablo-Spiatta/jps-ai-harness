# Convención: nombres de archivos y carpetas

Reglas de nomenclatura usadas en este repositorio. Antes de crear o renombrar rutas, aplicar esta tabla.

## Reglas generales

| Caso | Forma | Ejemplo |
| --- | --- | --- |
| Documentación y specs Markdown | `kebab-case.md` o nombre fijo corto en minúsculas | `file-naming.md`, `spec.md` |
| Roles de subagente | `snake_case.md` | `spec_author.md` |
| Carpetas de progreso por subagente | `snake_case/` (igual que el rol) | `sdd/progress/spec_author/` |
| Carpetas de feature SDD | `NNNN-feature-slug` (ver abajo) | `0001-user-login` |
| Historias de Usuario (backlog) | `US-NNN-<slug>.md` (ver abajo) | `US-001-user-login.md` |
| Carpetas de skills | `kebab-case/` | `.agents/skills/user-login/` |
| Archivo principal de una skill | `SKILL.md` | `.agents/skills/user-login/SKILL.md` |
| Agentes nativos (adaptadores) | `kebab-case` en el `name` y en el archivo según la herramienta | `spec-author` |

No mezclar estilos en el mismo ámbito (p. ej. no `Spec_Author.md` junto a `spec_author.md`).

## Specs SDD: `sdd/specs/<NNNN-feature-slug>/`

Fuente de detalle operativo: [`.agents/roles/leader.md`](../../.agents/roles/leader.md) (sección de artefactos de fase). Resumen:

| Parte | Regla | Ejemplo |
| --- | --- | --- |
| `NNNN` | Entero secuencial de 4 dígitos, con ceros a la izquierda | `0001` |
| `feature-slug` | kebab-case, ASCII minúsculas, sin espacios ni `_` | `user-login` |

Artefactos fijos dentro de la carpeta: `spec.md`, `plan.md`, `tasks.md`.

Válidos: `0001-user-login`, `0002-export-invoices`.  
Inválidos: `1-UserLogin`, `0001_user_login`, `0001-User Login`.

## Backlog SDD: `sdd/backlog/US-NNN-<slug>.md`

Fuente de detalle operativo: [`sdd/backlog/README.md`](../../sdd/backlog/README.md). Resumen:

| Parte | Regla | Ejemplo |
| --- | --- | --- |
| `US-NNN` | Prefijo `US-` + entero de 3 dígitos con ceros | `US-001` |
| `<slug>` | kebab-case ASCII, 2–5 palabras | `user-login` |
| Archivo | `US-NNN-<slug>.md` | `US-001-user-login.md` |

Plantilla: [`sdd/templates/backlog/us.md`](../../sdd/templates/backlog/us.md). Cada US es un archivo único; la cola ordenada vive en el `README.md` del backlog.

## Convenciones de este directorio

Los archivos bajo `docs/conventions/` usan **kebab-case** (`gitflow.md`, `file-naming.md`).

## Fuera de alcance

Nombres de código de producto (clases, módulos, paquetes) quedan en convenciones propias del producto cuando existan; este harness no las define aquí.
