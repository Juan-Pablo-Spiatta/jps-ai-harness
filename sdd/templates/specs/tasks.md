# Tasks — trabajo ejecutable

> Lo escribe **spec_author** en la fase Tasks.
> Destino: `sdd/specs/<NNNN-feature-slug>/tasks.md` (misma carpeta que la spec; ruta exacta en el brief).
> Se crea o actualiza **antes** del gate: el humano las revisa ahí en G3. La existencia del archivo no implica aprobación (P1).
> Parte de un **plan aprobado en G2**. Cada task debe ser accionable por el **implementer**.
> Gate: **G3**. No añadir alcance que no esté en el plan aprobado.
> P6: comportamiento ejecutable en orden TDD (red → green → refactor). Comando de verificación = el citado en el plan desde la decisión de pruebas bajo `docs/decisions/`.

## Identificación

| Campo | Valor |
| --- | --- |
| US / id | |
| Carpeta SDD | `sdd/specs/<NNNN-feature-slug>/` |
| Título | |
| Plan aprobado (ruta) | `sdd/specs/<NNNN-feature-slug>/plan.md` |
| Spec aprobada (ruta) | `sdd/specs/<NNNN-feature-slug>/spec.md` |
| Decisión de pruebas (ruta) | Ruta real bajo `docs/decisions/` (la citada en el plan) |
| Comando de test (citado del plan) | |
| Excepción TDD | `N/A` \| listar tasks o áreas fuera de TDD (según el plan) |
| Proyecto / paquete | |
| Estado | `draft` \| `needs_human` \| `ready_for_g3` \| `approved_g3` |
| Creadas | |
| Última actualización | |

## Formato de cada task

- **ID:** `T001`, `T002`, …
- **`[P]`** (opcional): puede ejecutarse en paralelo con otras `[P]` del mismo grupo (archivos distintos, sin dependencia mutua).
- Descripción concreta: acción + ruta o área verificable.
- Dependencias explícitas si las hay (`depends on T00x`).
- **TDD (P6):** por cada comportamiento ejecutable, un trío ordenado:
  - **Red:** escribir o ajustar el test y evidenciar que falla.
  - **Green:** código mínimo que hace pasar el test (`depends on` la task red).
  - **Refactor:** opcional; sin cambiar comportamiento (`depends on` la task green).

Ejemplo TDD:

```text
- [ ] T010 Red: test de Y en ruta/al/test (debe fallar)
- [ ] T011 Green: implementar Y en ruta/al/codigo (depends on T010)
- [ ] T012 Refactor: limpiar Y sin cambiar comportamiento (depends on T011)
```

Ejemplo fuera de TDD (solo si el plan declaró excepción): `- [ ] T020 Actualizar docs/decisions/architecture.md`

## Lista de tasks

### Grupo 1 — Preparación

**Objetivo:**

- [ ] T001
- [ ] T002 [P]

### Grupo 2 — [comportamiento / bloque del plan] (TDD)

**Objetivo:** un comportamiento ejecutable en red → green → refactor.

- [ ] T003 Red: …
- [ ] T004 Green: … (depends on T003)
- [ ] T005 Refactor: … (depends on T004)

### Grupo 3 — Verificación

**Objetivo:** evidenciar TDD y el resto de comprobaciones con el comando documentado.

- [ ] T00N Ejecutar el comando de test citado arriba; reportar evidencia de red (fallo esperado) y green (pase) por cada unidad TDD
- [ ] T00N+1 Ejecutar builds / linters existentes (si aplican) y reportar resultado real

## Orden y dependencias

| Task | Depende de | Notas |
| --- | --- | --- |
| T001 | — | |
| T002 | — | paralelo con T001 si ambas `[P]` |
| T003 | … | red |
| T004 | T003 | green |
| T005 | T004 | refactor |

## Criterio de hecho (DoD) del conjunto

> Cuándo el implementer puede marcar el encargo como `done` respecto a estas tasks.

-
- Todas las tasks marcadas o reportadas con evidencia
- Cada unidad TDD con evidencia de red (fallo) y green (pase) usando el comando citado
- Builds / linters existentes ejecutados si aplican; resultado real en el return
- Excepciones a TDD solo las declaradas en Identificación / plan

## Preguntas y riesgos abiertos

- (ninguno)

## Prohibiciones de esta fase

- No inventar alcance fuera del plan aprobado.
- No implementar aquí (eso es fase Implement).
- No omitir el desglose red→green→refactor para comportamiento ejecutable (P6), salvo excepción declarada.
- No inventar comando de test distinto al del plan / decisión bajo `docs/decisions/`.
- No marcar `approved_g3` ni asumir G3: eso lo registra el leader tras el «aprobado» explícito del humano.
