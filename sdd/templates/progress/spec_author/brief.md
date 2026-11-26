# Brief → spec_author

> Lo escribe el **leader** antes de delegar. El subagente no ve el chat: solo este brief, su rol y las rutas citadas.

## Encargo

| Campo | Valor |
| --- | --- |
| US / id | |
| Fase | Spec \| Plan \| Tasks |
| Rol | `.agents/roles/spec_author.md` |

## Rutas de entrada

| Entrada | Ruta |
| --- | --- |
| Backlog / US | |
| Spec aprobada | |
| Plan aprobado | |
| Tasks aprobadas | |
| Otro | |

## Ruta de salida (artefacto de fase)

> Bajo `sdd/specs/<NNNN-feature-slug>/`. El subagente escribe el archivo **antes** del gate para que el humano lo revise.

| Campo | Valor |
| --- | --- |
| Carpeta SDD | `sdd/specs/<NNNN-feature-slug>/` |
| Artefacto | spec.md \| plan.md \| tasks.md |
| Ruta completa | `sdd/specs/<NNNN-feature-slug>/<artefacto>` |
| Pisa / reemplaza (si aplica) | `sdd/specs/<NNNN-feature-slug>/` supersedida, o vacío |

## Return

Escribir el resultado en: `sdd/progress/spec_author/return.md`

## Feedback del humano

> Completar solo en reintentos tras gate rechazado o tras resolver preguntas.

-

## Prohibiciones

- No inventar requisitos.
- Toda duda o riesgo se reporta en el return; no avanzar como si estuviera resuelto (P5).
- No modificar artefactos fuera de la responsabilidad de este rol.
