# jps-ai-harness

Harness de **Spec-Driven Development (SDD)** con agentes de IA. Es **agnóstico de producto**: sirve de base para un repo simple o un monorepo. Lo propio de un producto concreto (stack, arquitectura, pruebas) se completa al adoptarlo.

La metodología vive en [`constitution.md`](./constitution.md). Los agentes automatizados deben empezar por [`AGENTS.MD`](./AGENTS.MD) (este README es solo para personas).

## Ciclo SDD

```text
US (backlog) → Spec → G1 → Plan → G2 → Tasks → G3 → Implement → Review → G4
```

- Cada spec sale de una Historia de Usuario del backlog.
- Los gates **G1–G4** los aprueba únicamente un humano.
- Comportamiento ejecutable se introduce con **TDD** (P6); el stack de pruebas se documenta bajo `docs/decisions/`.

## Mapa del repositorio

| Ruta | Contenido |
| --- | --- |
| [`constitution.md`](./constitution.md) | Principios (P1–P6), ciclo, gates y roles |
| [`AGENTS.MD`](./AGENTS.MD) | Entrada obligatoria para agentes (reglas + glosario) |
| [`.agents/roles/`](./.agents/roles/) | Roles: `leader`, `spec_author`, `implementer`, `reviewer`, `explorer`, `git_flow` |
| [`.agents/agents_adapter.md`](./.agents/agents_adapter.md) | Cómo publicar cada rol en Copilot, Claude Code, Cursor y Codex |
| [`sdd/backlog/`](./sdd/backlog/README.md) | Historias de Usuario (`US-NNN-<slug>.md`) y cola ordenada |
| [`sdd/templates/`](./sdd/templates/) | Plantillas de backlog, specs y progreso del ciclo |
| `sdd/specs/<NNNN-feature-slug>/` | Artefactos de fase: `spec.md`, `plan.md`, `tasks.md` (se crean al trabajar una US) |
| `sdd/progress/` | Estado del ciclo en curso (lo mantiene el `leader`) |
| [`docs/conventions/`](./docs/conventions/) | Forma del harness: nombres, GitFlow, skills |
| [`docs/decisions/`](./docs/decisions/) | Decisiones de producto (arquitectura, stacks, testing) |
| [`.gitignore`](./.gitignore) | Secretos, IDE, caches y artefactos locales |

## Roles

| Rol | Qué hace |
| --- | --- |
| `leader` | Orquesta el ciclo, briefs/returns y gates; no aprueba ni escribe artefactos de fase |
| `spec_author` | Spec, plan y tasks a partir de la US / artefactos aprobados |
| `implementer` | Ejecuta las tasks aprobadas (TDD cuando hay comportamiento ejecutable) |
| `reviewer` | Revisa contra spec, plan, tasks y constitution |
| `explorer` | Recopila información a demanda |
| `git_flow` | Ramas, publicación y merge requests según la convención GitFlow |

## Cómo usarlo (humano)

1. Copiá o cloná este harness en el repo del producto.
2. Completá las decisiones de producto bajo [`docs/decisions/`](./docs/decisions/) (al menos el stack de pruebas si habrá comportamiento ejecutable).
3. Escribí US en [`sdd/backlog/`](./sdd/backlog/README.md) (plantilla en `sdd/templates/backlog/us.md`) y registralas en la cola del README del backlog.
4. Pedile al agente que arranque el ciclo SDD de una US; el `leader` orquesta el resto.
5. Aprobá o rechazá explícitamente cada gate (G1–G4).

## Estado actual

- Harness listo: constitution, roles, adaptador, plantillas, backlog, convenciones y `.gitignore`.
- Cola del backlog vacía (sin US de producto todavía).
- `docs/decisions/testing-stacks.md` es plantilla reservada: hay que completar o reemplazar al llevarlo a un producto real.
- Aún no hay carpetas activas bajo `sdd/specs/` ni `sdd/progress/` (se crean al iniciar un ciclo).
