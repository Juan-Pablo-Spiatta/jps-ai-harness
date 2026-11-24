# Decisiones de producto

Documentación de **decisiones del producto**: arquitectura, stacks tecnológicos, testing, y otras elecciones técnicas equivalentes. No es metodología SDD ni convenciones de forma del harness.

## Cómo usar este directorio

| Quién | Qué hace |
| --- | --- |
| Humanos | Definen o enmiendan aquí las decisiones del producto al adoptar el harness o cuando cambian. |
| Agentes | Si el humano pide documentar algo del producto (arquitectura, stacks, testing, etc.), lo crean o actualizan **solo** en esta carpeta. Consultan estas decisiones antes de planificar o implementar. |

- Un tema = un archivo Markdown en esta carpeta.
- Nombre del archivo: **kebab-case** + `.md` (el producto elige el nombre; p. ej. `testing-stacks.md`, `architecture.md`).
- Para TDD (P6) debe existir aquí alguna decisión que documente stack de pruebas y cómo usarlos. Si no existe o está incompleta, el agente lo exige al humano (P5); no inventa el contenido ni otra carpeta.

## Índice

| Archivo | Tema |
| --- | --- |
| [testing-stacks.md](./testing-stacks.md) | Plantilla de ejemplo para documentar stack de pruebas (el nombre final lo define el producto) |

## Precedencia

- `AGENTS.MD` y `constitution.md` mandan sobre estas decisiones.
- Estas decisiones mandan sobre hábitos ad hoc al documentar o elegir stack/arquitectura del producto.
- Si hay conflicto entre decisiones, o entre una decisión y un rol, el agente se detiene y lo comunica al humano (P5).
