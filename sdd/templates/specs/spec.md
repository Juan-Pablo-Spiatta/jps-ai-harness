# Spec — qué y por qué

> Lo escribe **spec_author** en la fase Spec.
> Destino: `sdd/specs/<NNNN-feature-slug>/spec.md` (ruta exacta en el brief).
> Se crea o actualiza **antes** del gate: el humano la revisa ahí en G1. La existencia del archivo no implica aprobación (P1).
> Define solo el **qué** y el **por qué**. El **cómo** va en `plan.md` (P2, constitution §2).
> Gate: **G1**. No marcar lista para G1 si quedan preguntas o riesgos abiertos (P5).

## Identificación

| Campo | Valor |
| --- | --- |
| US / id | |
| Carpeta SDD | `sdd/specs/<NNNN-feature-slug>/` |
| Título | |
| Proyecto / paquete | |
| Origen (ruta US / backlog) | |
| Estado | `draft` \| `needs_human` \| `ready_for_g1` \| `approved_g1` |
| Creada | |
| Última actualización | |

## Origen

> Toda spec sale de una US del backlog (constitution §2). No inventar requisitos.

- **US / id:**
- **Texto o resumen de la US:**
- **Alcance de esta spec:** (si la US afecta varios proyectos/paquetes, una spec por cada uno)

## Problema y por qué

> Motivación y valor. Sin decisiones técnicas.

-

## Qué se quiere

> Capacidad o resultado observable. Sin el cómo.

-

## Escenarios de aceptación

> Criterios verificables en lenguaje de producto (Given / When / Then u equivalente).

### Escenario 1 — [título]

1. **Given** [estado inicial], **When** [acción], **Then** [resultado esperado]

### Escenario 2 — [título]

1. **Given** [estado inicial], **When** [acción], **Then** [resultado esperado]

### Casos límite

- Qué ocurre cuando [condición límite]
- Cómo se comporta ante [error o vacío]

## Requisitos funcionales

> Solo comportamiento y reglas de producto. Marcar con `NEEDS CLARIFICATION` lo ambiguo.

- **RF-001:**
- **RF-002:**

## Criterios de éxito

> Resultados medibles o comprobables sin presuponer implementación.

- **CE-001:**
- **CE-002:**

## Fuera de alcance

-

## Supuestos

> Solo supuestos confirmados con el humano o explícitos en la US. Si es duda → sección siguiente.

-

## Preguntas y riesgos abiertos

> Debe quedar vacío (o resuelto) antes de pedir G1. Si hay ítems, return `needs_human`.

- (ninguno)

## Prohibiciones de esta fase

- No incluir stack, APIs, esquemas, librerías ni diseño técnico.
- No ampliar el alcance más allá de la US y de las respuestas del humano.
- No marcar `approved_g1` ni asumir G1: eso lo registra el leader tras el «aprobado» explícito del humano.
