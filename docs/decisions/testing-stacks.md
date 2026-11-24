# Stack de pruebas

> **Plantilla de ejemplo** bajo `docs/decisions/`. El producto puede usar este archivo o otro nombre kebab-case en la misma carpeta.
> **RESERVADO** hasta completar al llevar el harness a un producto real.
> Hasta que *alguna* decisión bajo `docs/decisions/` defina stack, comando(s) y ubicación de tests, un plan con comportamiento ejecutable no está listo para G2 (constitution P6): el agente lo exige al humano.
> Los agentes no inventan runner ni comando: solo usan lo documentado en esa decisión.

## Identificación

| Campo | Valor |
| --- | --- |
| Estado | `reserved` \| `draft` \| `active` |
| Producto / paquete | |
| Última actualización | |

## Stack

> Framework(s) o runner(s) de pruebas del producto. Sin nombres inventados: solo lo adoptado de verdad.

| Campo | Valor |
| --- | --- |
| Runner / framework | TODO |
| Lenguaje / runtime | TODO |
| Dependencias de test relevantes | TODO |

## Cómo ejecutar

> Comando(s) verificables que el implementer y el reviewer deben usar. Copiar literalmente al plan.

| Uso | Comando |
| --- | --- |
| Suite completa | TODO |
| Archivo o test concreto | TODO |
| Watch / iteración TDD (si aplica) | TODO o `N/A` |

## Dónde viven los tests

> Rutas o convención de ubicación (p. ej. `tests/`, `*.test.ts` junto al código).

-

## Cómo escribir pruebas bajo TDD

> Convenciones mínimas del producto: naming, qué se mockea, niveles (unit/integration), etc.

-

## Fuera de TDD

> Tipos de cambio que el producto trata como excepción a P6 (si los hay). El plan y las tasks deben declarar la excepción caso a caso.

- Documentación, renames y configuración sin lógica (excepción por defecto del harness).
- (añadir otras del producto, si aplica)

## Notas

-
