# Brief → git_flow

> Lo escribe el **leader** (u otro agente que lo invoque) antes de delegar. El subagente no ve el chat: solo este brief, su rol y las rutas citadas.

## Encargo

| Campo | Valor |
| --- | --- |
| US / id (si aplica) | |
| Alcance | A demanda (GitFlow) |
| Rol | `.agents/roles/git_flow.md` |

## Operación pedida

| Campo | Valor |
| --- | --- |
| Operación | `start_branch` \| `publish_branch` \| `open_mr` \| `status` \| (otra explícita) |
| Tipo de rama | `feature` \| `bugfix` \| `release` \| `hotfix` \| `support` |
| Slug / nombre | |
| Base (si no es la habitual) | |
| Destino del MR (si aplica) | `dev` \| `main` \| … |
| ¿Commit autorizado? | no \| sí (mensaje:) |
| ¿Push autorizado? | no \| sí |
| ¿Abrir MR autorizado? | no \| sí |

## Contexto para el MR (si aplica)

| Campo | Valor |
| --- | --- |
| Título sugerido | |
| Spec / decisión a referenciar | |
| Etiquetas / milestone | |
| Validaciones a mencionar | |

## Return

Escribir el resultado en: `sdd/progress/git_flow/return.md`

## Feedback del humano

> Completar solo si el humano acotó la operación o autorizó un paso pendiente.

-

## Prohibiciones

- No inventar bases, destinos de MR ni prefijos fuera de [docs/conventions/gitflow.md](../../../../docs/conventions/gitflow.md).
- No push/force push a `main` o `dev`; no crear tags de versión.
- No modificar artefactos de fase ni `current.md` / `history.md`.
- Commit, push y abrir MR solo si este brief los autoriza de forma explícita (P5).
