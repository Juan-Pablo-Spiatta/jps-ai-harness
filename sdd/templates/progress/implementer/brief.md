# Brief → implementer

> Lo escribe el **leader** antes de delegar. El subagente no ve el chat: solo este brief, su rol y las rutas citadas.

## Encargo

| Campo | Valor |
| --- | --- |
| US / id | |
| Fase | Implement |
| Rol | `.agents/roles/implementer.md` |

## Rutas de entrada

| Entrada | Ruta |
| --- | --- |
| Spec aprobada | `sdd/specs/<NNNN-feature-slug>/spec.md` |
| Plan aprobado | `sdd/specs/<NNNN-feature-slug>/plan.md` |
| Tasks aprobadas | `sdd/specs/<NNNN-feature-slug>/tasks.md` |
| Otro | |

## Ruta de salida (artefacto de fase)

| Artefacto | Ruta esperada |
| --- | --- |
| Implementación | |

## Return

Escribir el resultado en: `sdd/progress/implementer/return.md`

## Feedback del humano

> Completar solo en reintentos tras gate rechazado o tras resolver preguntas.

-

## Prohibiciones

- No inventar requisitos.
- Toda duda o riesgo se reporta en el return; no avanzar como si estuviera resuelto (P5).
- No modificar artefactos fuera de la responsabilidad de este rol.
- No cambiar spec, plan o tasks ya aprobados; si hace falta, reportarlo (P4).
