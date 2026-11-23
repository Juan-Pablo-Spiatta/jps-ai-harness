# Plan — cómo

> Lo escribe **spec_author** en la fase Plan.
> Destino: `sdd/specs/<NNNN-feature-slug>/plan.md` (misma carpeta que la spec; ruta exacta en el brief).
> Se crea o actualiza **antes** del gate: el humano lo revisa ahí en G2. La existencia del archivo no implica aprobación (P1).
> Parte de una **spec aprobada en G1**. Define el **cómo** sin reescribir ni contradecir la spec (P2, P4).
> Gate: **G2**. Antes de pedir G2, completar el contraste con la constitution (sección 4).

## Identificación

| Campo | Valor |
| --- | --- |
| US / id | |
| Carpeta SDD | `sdd/specs/<NNNN-feature-slug>/` |
| Título | |
| Spec aprobada (ruta) | `sdd/specs/<NNNN-feature-slug>/spec.md` |
| Proyecto / paquete | |
| Estado | `draft` \| `needs_human` \| `ready_for_g2` \| `approved_g2` |
| Creado | |
| Última actualización | |

## Resumen

> Enfoque técnico en pocas líneas, anclado a la spec aprobada.

-

## Contexto técnico

| Campo | Valor |
| --- | --- |
| Lenguaje / runtime | |
| Dependencias relevantes | |
| Persistencia | |
| Pruebas | |
| Plataforma / entorno | |
| Restricciones | |
| Escala / alcance técnico | |

> Si un campo no aplica: `N/A`. Si falta información crítica: `NEEDS CLARIFICATION` y reportarlo en preguntas.

## Contraste con la constitution

> Obligatorio antes de G2 (constitution §4). Una violación es bloqueante: corregir el plan o reportar `needs_human`; no reinterpretar el principio.

| Principio / regla | ¿Cumple? | Evidencia / nota |
| --- | --- | --- |
| P1 — Solo un humano aprueba | sí \| no \| N/A | |
| P2 — Sin saltos en el ciclo | sí \| no \| N/A | |
| P3 — Un responsable por artefacto | sí \| no \| N/A | |
| P4 — Lo aprobado solo se cambia reabriendo | sí \| no \| N/A | |
| P5 — Las dudas se preguntan | sí \| no \| N/A | |
| Ciclo Spec → … → G4 | sí \| no \| N/A | |
| Otros (P6+ del producto, si existen) | sí \| no \| N/A | |

**Resultado del contraste:** `pass` \| `fail` \| `needs_human`

**Violaciones / acciones:**

- (ninguna)

## Enfoque de implementación

> Decisiones de diseño y pasos de alto nivel. Sin lista de tasks (eso es `tasks.md`).

1.
2.
3.

## Estructura afectada

> Rutas reales del repo o estructura prevista. No inventar rutas no verificadas.

```text
# Árbol o lista de áreas a tocar
```

**Decisión de estructura:**

-

## Riesgos técnicos y dependencias

-

## Preguntas y riesgos abiertos

> Resolver con el humano antes de G2 si bloquean el plan.

- (ninguno)

## Prohibiciones de esta fase

- No contradecir ni reescribir la spec aprobada; si hace falta cambiarla, reportar P4.
- No redactar las tasks aquí.
- No marcar `approved_g2` ni asumir G2: eso lo registra el leader tras el «aprobado» explícito del humano.
