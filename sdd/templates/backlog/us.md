# US-NNN — <título corto>

> Plantilla de Historia de Usuario. Copiar a `sdd/backlog/US-NNN-<slug>.md`.
> La escribe un **humano** (o se copia desde una fuente acordada). Los agentes no inventan US.
> Es el **origen** de la fase Spec (constitution §2). Define valor y alcance en lenguaje de producto.
> El **qué detallado** y los criterios verificables finos van en `sdd/specs/.../spec.md` (G1).
> El **cómo** no va acá: va en el plan.

## Identificación

| Campo | Valor |
| --- | --- |
| US / id | `US-NNN` |
| Archivo | `sdd/backlog/US-NNN-<slug>.md` |
| Título | |
| Estado | `ready` \| `in_refinement` \| `in_progress` \| `done` \| `blocked` |
| Prioridad en cola | (posición en [sdd/backlog/README.md](../../backlog/README.md); 1 = siguiente) |
| Creada | YYYY-MM-DD |
| Última actualización | YYYY-MM-DD |

## Historia

> Formato clásico. Una sola capacidad por US.

**Como** [rol / actor],
**quiero** [capacidad o resultado],
**para** [valor de negocio u operacional].

## Contexto

> Por qué importa ahora. Sin diseño técnico.

-

## Alcance

### Artefactos afectados

> Directorios, proyectos o paquetes del repositorio que la US puede tocar. Una US que afecta varios genera **una spec por cada uno** (constitution §2). Completar la tabla al llevar el harness a un producto real.

| Artefacto | ¿Afecta? | Nota breve |
| --- | --- | --- |
| (definir) | sí \| no | |

### En alcance

-

### Fuera de alcance

-

## Criterios de aceptación (borrador)

> Criterios de producto, verificables a alto nivel. La spec los refinará como escenarios Given/When/Then y `AC-NNN-MM`.

- [ ] **CA-01:**
- [ ] **CA-02:**
- [ ] **CA-03:**

## Fuentes

> Enlaces a vault, MVP, decisiones bajo `docs/decisions/` o specs hermanas. Rutas relativas desde este archivo.

-

## Dependencias

> Otras US, specs, repos o decisiones que deben existir o estar resueltas antes.

-

## Preguntas abiertas

> Si hay ítems, la US no debería entrar al ciclo sin resolución humana (P5).

- (ninguno)
