# backlog/ — Historias de Usuario

Origen de cada ciclo SDD (constitution §2): **toda spec sale de una US de este backlog**.

Las US se toman **en el orden de la cola** de abajo. El `leader` cita la ruta del archivo US en el brief; `spec_author` no inventa requisitos fuera de la US y de las respuestas del humano.

## Crear una US

1. Copiá [../templates/backlog/us.md](../templates/backlog/us.md) a `US-NNN-<slug>.md` (número de 3 dígitos siguiente libre; slug en kebab-case).
2. Completá identificación, historia, alcance (artefactos afectados), criterios borrador y fuentes.
3. Agregá la fila a la **cola** de este README, en la posición de prioridad acordada.
4. No marques `in_progress` / `done` desde el archivo solo: el estado del ciclo vive en [../progress/current.md](../progress/current.md); al cerrar G4, actualizá la fila y el estado de la US.

## Cola (orden de trabajo)

| Orden | US | Título | Estado | Spec(s) |
| --- | --- | --- | --- | --- |
| — | — | *(vacía — agregar US al llevar el harness a un producto)* | — | — |

## Convención de nombres

| Parte | Regla | Ejemplo |
| --- | --- | --- |
| `US-NNN` | Prefijo `US-` + entero de 3 dígitos con ceros | `US-001` |
| `<slug>` | kebab-case ASCII, 2–5 palabras | `user-login` |
| Archivo | `US-NNN-<slug>.md` | `US-001-user-login.md` |

Estados del archivo US: `ready` (en cola), `in_refinement` (en refinamiento: aclarar alcance, criterios o fuentes antes del ciclo), `in_progress` (ciclo SDD activo), `done` (G4 aprobado), `blocked` (dependencia o pregunta abierta).
