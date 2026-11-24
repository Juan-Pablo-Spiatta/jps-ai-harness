# Convenciones

Acuerdos de **forma** del repositorio (harness): cómo se nombran cosas, cómo se escriben commits, y reglas similares que no son metodología SDD, principios de la constitution ni decisiones de producto.

## Cómo usar este directorio

| Quién | Qué hace |
| --- | --- |
| Humanos | Definen o enmiendan convenciones aquí. |
| Agentes | Las consultan antes de crear, renombrar o formatear artefactos sujetos a ellas. |

- Un tema = un archivo Markdown en esta carpeta.
- Nombre del archivo: **kebab-case** + `.md` (ej. `file-naming.md`, `commits.md`).
- Si una convención aún no existe o está vacía, el agente lo indica y pregunta al humano (P5); no inventa una.

## Índice

| Archivo | Tema |
| --- | --- |
| [file-naming.md](./file-naming.md) | Nombres de archivos y carpetas |
| [commits.md](./commits.md) | Formato de mensajes de commit |

## Precedencia

- `AGENTS.MD` y `constitution.md` mandan sobre estas convenciones.
- Estas convenciones mandan sobre hábitos ad hoc al crear o renombrar contenido del repo.
- Si hay conflicto entre convenciones, o entre una convención y un rol, el agente se detiene y lo comunica al humano (P5).
