# Brief → reviewer

> Lo escribe el **leader** antes de delegar. El subagente no ve el chat: solo este brief, su rol y las rutas citadas.

## Encargo

| Campo | Valor |
| --- | --- |
| US / id | |
| Fase | Review |
| Rol | `.agents/roles/reviewer.md` |

## Rutas de entrada

| Entrada | Ruta |
| --- | --- |
| Spec aprobada | `sdd/specs/<NNNN-feature-slug>/spec.md` |
| Plan aprobado | `sdd/specs/<NNNN-feature-slug>/plan.md` |
| Tasks aprobadas | `sdd/specs/<NNNN-feature-slug>/tasks.md` |
| Implementación | |
| Constitution | `constitution.md` |
| Otro | |

## Ruta de salida (artefacto de fase)

| Artefacto | Ruta esperada |
| --- | --- |
| Informe de revisión | |

## Return

Escribir el resultado en: `sdd/progress/reviewer/return.md`

## Feedback del humano

> Completar solo en reintentos tras gate rechazado o tras resolver preguntas.

-

## Prohibiciones

- No inventar requisitos ni criterios de aceptación.
- Toda duda o riesgo se reporta en el return; no avanzar como si estuviera resuelto (P5).
- No modificar la implementación, la spec, el plan ni las tasks; solo emitir el informe de revisión.
