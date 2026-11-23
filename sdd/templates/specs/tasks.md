# Tasks — trabajo ejecutable

> Lo escribe **spec_author** en la fase Tasks.
> Destino: `sdd/specs/<NNNN-feature-slug>/tasks.md` (misma carpeta que la spec; ruta exacta en el brief).
> Se crea o actualiza **antes** del gate: el humano las revisa ahí en G3. La existencia del archivo no implica aprobación (P1).
> Parte de un **plan aprobado en G2**. Cada task debe ser accionable por el **implementer**.
> Gate: **G3**. No añadir alcance que no esté en el plan aprobado.

## Identificación

| Campo | Valor |
| --- | --- |
| US / id | |
| Carpeta SDD | `sdd/specs/<NNNN-feature-slug>/` |
| Título | |
| Plan aprobado (ruta) | `sdd/specs/<NNNN-feature-slug>/plan.md` |
| Spec aprobada (ruta) | `sdd/specs/<NNNN-feature-slug>/spec.md` |
| Proyecto / paquete | |
| Estado | `draft` \| `needs_human` \| `ready_for_g3` \| `approved_g3` |
| Creadas | |
| Última actualización | |

## Formato de cada task

- **ID:** `T001`, `T002`, …
- **`[P]`** (opcional): puede ejecutarse en paralelo con otras `[P]` del mismo grupo (archivos distintos, sin dependencia mutua).
- Descripción concreta: acción + ruta o área verificable.
- Dependencias explícitas si las hay (`depends on T00x`).

Ejemplo: `- [ ] T012 [P] Crear modelo X en ruta/al/archivo` · `- [ ] T014 Implementar servicio Y (depends on T012)`

## Lista de tasks

### Grupo 1 — Preparación

**Objetivo:**

- [ ] T001
- [ ] T002 [P]

### Grupo 2 — [nombre del bloque del plan]

**Objetivo:**

- [ ] T003
- [ ] T004 [P]
- [ ] T005 (depends on T003)

### Grupo 3 — Verificación

**Objetivo:** comprobar lo exigido por el plan con las herramientas existentes del repo.

- [ ] T00N Ejecutar builds / tests / linters existentes y reportar resultado real

## Orden y dependencias

| Task | Depende de | Notas |
| --- | --- | --- |
| T001 | — | |
| T002 | — | paralelo con T001 si ambas `[P]` |
| T003 | T001 | |

## Criterio de hecho (DoD) del conjunto

> Cuándo el implementer puede marcar el encargo como `done` respecto a estas tasks.

-
- Todas las tasks marcadas o reportadas con evidencia
- Builds / tests / linters existentes ejecutados; resultado real en el return

## Preguntas y riesgos abiertos

- (ninguno)

## Prohibiciones de esta fase

- No inventar alcance fuera del plan aprobado.
- No implementar aquí (eso es fase Implement).
- No marcar `approved_g3` ni asumir G3: eso lo registra el leader tras el «aprobado» explícito del humano.
