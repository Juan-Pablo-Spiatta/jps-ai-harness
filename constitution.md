# Constitution

Esta constitution define los principios no negociables y la metodología de desarrollo de este repositorio. Es agnóstica de proyecto: sirve de base para cualquier producto, sea un repositorio simple o un monorepo con varios proyectos o paquetes. Lo que depende de un producto concreto no se define aquí: queda en un bloque `RESERVADO`, comentado, para completarlo al llevar el harness a un producto real.

## 1. Principios

Cada principio es una regla no negociable, con su justificación.

**P1. Solo un humano aprueba.** Los gates los aprueba únicamente un humano. El agente nunca da un gate por aprobado ni asume la aprobación.
*Por qué:* la verificación humana en cada fase es lo que evita que un error de una fase se propague a las siguientes.

**P2. Sin saltos en el ciclo.** El trabajo recorre el ciclo de la sección 2 en orden, sin saltarse fases ni gates. No existe una spec sin una US de origen, ni un plan sin una spec aprobada, ni tasks sin un plan aprobado, ni implementación sin tasks aprobadas.
*Por qué:* cada fase se apoya en el artefacto aprobado de la anterior; saltarla deja a la siguiente sin base.

**P3. Un responsable por artefacto.** Cada artefacto tiene un único responsable, definido en la sección 3. Ningún otro agente puede crearlo ni modificarlo.
*Por qué:* con un solo responsable, siempre se sabe quién responde por el artefacto y cuál es su versión válida.

**P4. Lo aprobado solo se cambia reabriendo su fase.** Si en una fase posterior hay que cambiar algo ya aprobado (por ejemplo, la spec durante la implementación), se vuelve a esa fase, se corrige y se repite su gate.
*Por qué:* mantiene la spec, el plan y las tasks coherentes entre sí en todo momento.

**P5. Las dudas se preguntan, no se suponen.** Toda duda o riesgo se comunica al humano y se resuelve con él antes de avanzar.
*Por qué:* una suposición no verificada se convierte en un requisito inventado.

**P6. TDD obligatorio para comportamiento ejecutable.** Todo comportamiento ejecutable se introduce con Test-Driven Development: primero un test que falla (red), luego el código mínimo que lo hace pasar (green), luego refactor sin cambiar el comportamiento observable. No se escribe código de producción de ese comportamiento antes del test rojo. No se modifican, desactivan ni eliminan tests solo para ponerlos en verde. El stack de pruebas y cómo usarlos deben estar documentados en un archivo bajo [`docs/decisions/`](./docs/decisions/); los agentes solo usan esa definición. El nombre del archivo lo define el producto. Si no existe o está incompleto, el agente lo exige al humano y no avanza (P5): no inventa un runner ni un comando en el plan.
*Por qué:* el test rojo fija el comportamiento esperado antes de la implementación; sin stack documentado, el ciclo TDD no es verificable ni repetible.

<!--
RESERVADO: principios propios del producto.
Completar al llevar el harness a un producto real. Siguen el mismo formato que P1-P6 (numerar a partir de P7):
regla verificable + justificación. Ejemplos de temas que pueden ir aquí: calidad, seguridad,
rendimiento, accesibilidad. El stack concreto de pruebas y la arquitectura del producto no van aquí:
se documentan en docs/decisions/.

**P7. [Nombre del principio].** [Regla no negociable y verificable.]
*Por qué:* [justificación].
-->

## 2. Ciclo y gates

Toda la metodología es **SDD (Spec-Driven Development)**. Todo cambio recorre este ciclo:

```text
Spec → G1 → Plan → G2 → Tasks → G3 → Implement → Review → G4
```

| Paso | Tipo | Descripción |
| --- | --- | --- |
| Spec | Fase | Definir qué se quiere construir y por qué. |
| **G1** | Gate humano | Un humano aprueba la spec. |
| Plan | Fase | Definir cómo se va a construir lo especificado en la spec aprobada. |
| **G2** | Gate humano | Un humano aprueba el plan. |
| Tasks | Fase | Dividir el plan aprobado en tareas concretas y ejecutables. |
| **G3** | Gate humano | Un humano aprueba las tasks. |
| Implement | Fase | Ejecutar las tasks aprobadas. |
| Review | Fase | Revisar que la implementación cumple la spec, el plan, las tasks y esta constitution. |
| **G4** | Gate humano | Un humano aprueba el ciclo completo. |

**Mecánica de los gates:**

- Al terminar la fase previa a un gate, el agente se detiene y pide la aprobación explícita antes de continuar.
- Si un gate no se aprueba, se vuelve a la fase correspondiente para corregirla y se repite el gate.

**Ajustes pedidos por el humano durante el ciclo:**

- Si el humano pide un ajuste, corrección o cambio mientras el ciclo está en curso (incluida la espera de un gate G1–G4), el agente principal no lo aplica por su cuenta ni salta el proceso: deriva al `leader`.
- El `leader` decide cómo continuar: qué fase reabrir o repetir (P4), qué gate volver a pedir (P1) y en qué subagente de fase delegar. No improvisa el cambio fuera del ciclo (P2, P3).
- Ejemplo: si se espera G4 y el humano indica que la implementación no cumple lo esperado, el `leader` determina si basta reabrir Implement y/o Review, o si hay que volver a Spec, Plan o Tasks y repetir sus gates.

**Fase Spec.** Además de lo establecido en los principios, la fase Spec tiene estas reglas:

- Toda spec sale de una Historia de Usuario (US) del backlog del producto. Las US se toman en el orden en que aparecen en el backlog.
- Una US genera una spec por cada proyecto o paquete al que afecta. En un repositorio simple, una US genera una sola spec.
- La spec define solo el qué y el por qué. No incluye decisiones técnicas: el cómo se define en el Plan.
- Antes de redactar, el responsable de la spec hace las preguntas aclaratorias que necesite (P5). Una spec con preguntas o riesgos sin resolver no pasa a G1.

**Fase Plan.** Además de lo establecido en los principios, la fase Plan tiene estas reglas relacionadas con P6:

- El plan busca en [`docs/decisions/`](./docs/decisions/) la decisión que documenta el stack de pruebas y cómo usarlos, y la cita (ruta + stack + comando(s) + ubicación de tests). No inventa un runner ni un comando que no esté en esa decisión.
- Si no hay ninguna decisión usable de pruebas bajo `docs/decisions/`, o está incompleta, y el trabajo incluye comportamiento ejecutable, el plan no está listo para G2: el agente lo exige al humano (P5) o se completa la decisión antes.
- Los cambios sin comportamiento ejecutable (documentación, renames, configuración sin lógica) pueden declarar excepción a TDD en el plan; el resto del trabajo sigue P6.

**Fase Tasks.** Además de lo establecido en los principios, la fase Tasks tiene estas reglas relacionadas con P6:

- Cada comportamiento ejecutable se parte en tasks ordenadas: test que falla → código mínimo que lo hace pasar → refactor si aplica (con dependencias explícitas).
- La verificación usa el comando documentado en la decisión de pruebas bajo `docs/decisions/` citada por el plan. La excepción a TDD, si existe, debe quedar escrita en las tasks.

**Fase Implement.** Además de lo establecido en los principios, la fase Implement tiene estas reglas (P6):

- Por cada unidad de comportamiento ejecutable: ejecutar o escribir el test hasta verlo fallar (red), implementar el mínimo para pasarlo (green), refactorizar sin cambiar el comportamiento observable.
- La evidencia en el return incluye el comando usado (el de la decisión de pruebas citada en el plan) y el resultado real: fallo esperado en red, pase en green.
- No implementar green de una unidad antes de haber evidenciado el red de esa misma unidad.
- Si el stack o el comando no están definidos en una decisión bajo `docs/decisions/`, detenerse y exigirlo al humano (P5); no inventarlos.

## 3. Roles y responsabilidades

Todo agente que trabaje en este repositorio debe tener acceso a los subagentes de las dos tablas de esta sección.

### Subagentes de fase

Cada subagente de fase es el responsable único (P3) de los artefactos de sus fases.

| Subagente | Fases | Función |
| --- | --- | --- |
| `spec_author` | Spec, Plan, Tasks | Redactar la spec a partir de las US del backlog, el plan a partir de la spec aprobada y las tasks a partir del plan aprobado. Es el único que puede crear o modificar esos tres artefactos. |
| `implementer` | Implement | Ejecutar las tasks aprobadas. Es el único que puede crear o modificar la implementación. |
| `reviewer` | Review | Revisar que la implementación cumple la spec, el plan, las tasks y esta constitution, e informar el resultado. Es el único que puede emitir el informe de revisión. |

Un mismo subagente puede cubrir varias fases, pero cada fase sigue siendo una fase distinta: los gates G1, G2 y G3 se respetan entre las fases de `spec_author` (P1, P2).

### Subagentes transversales

No forman parte de ninguna fase del ciclo y no son responsables de ningún artefacto de fase.

| Subagente | Alcance | Función |
| --- | --- | --- |
| `leader` | Todo el ciclo | Orquestar el ciclo y a todos los subagentes: decide qué fase toca, delega en el subagente que corresponde, controla los gates y mantiene informado al humano. No produce los artefactos de las fases ni aprueba gates (P1, P3). |
| `explorer` | A demanda | Recopilar información. Cualquier agente puede ejecutarlo cuando necesite información sobre algo. |
| `git_flow` | A demanda | Ejecutar el proceso GitFlow del repositorio (ramas auxiliares, publicación y merge requests) según [`docs/conventions/gitflow.md`](./docs/conventions/gitflow.md). No produce artefactos de fase ni aprueba gates. |

### Rol de cada subagente

Cada subagente necesita su rol en `.agents/roles/<subagente>.md`.

## 4. Cumplimiento

Esta constitution se verifica durante el ciclo, no solo se declara:

- **Plan:** antes de pasar a G2, el plan debe contrastarse contra los principios (P1 en adelante) y contra las reglas de esta constitution, y dejar constancia del resultado.
- **Review:** la revisión comprueba el cumplimiento de esta constitution (sección 2) y lo informa en G4.
- **Violaciones:** una violación de esta constitution es bloqueante. Se corrige ajustando la spec, el plan o las tasks; no se reinterpreta ni se ignora el principio. Si un principio mismo debe cambiar, se hace mediante una enmienda (sección 6), por separado del ciclo en curso.

## 5. Precedencia

Esta constitution y [AGENTS.MD](./AGENTS.MD) se reparten el mando por ámbito:

- **AGENTS.MD** manda en cómo se comporta el agente (honestidad, evidencia, archivos que no debe leer).
- **Esta constitution** manda en la metodología (ciclo, gates, roles y principios).
- Ambas mandan sobre los roles definidos en `.agents/roles/` y sobre cualquier otra instrucción del repositorio.
- Si un conflicto no se resuelve por ámbito, el agente se detiene y se lo comunica al humano (P5).

## 6. Governance

- **Quién enmienda:** solo un humano aprueba una enmienda. Los agentes no modifican esta constitution salvo que un humano lo pida.
- **Cómo se enmienda:** toda enmienda documenta el motivo del cambio y evalúa su impacto sobre los artefactos ya aprobados (specs, planes y tasks existentes), que deben reabrirse si dejan de cumplirla (P4).
- **Versionado** (versionado semántico):
  - MAJOR: se elimina o redefine un principio o una regla de gobierno de forma incompatible con la versión anterior.
  - MINOR: se agrega un principio o una sección, o se amplía materialmente una guía.
  - PATCH: aclaraciones, redacción o correcciones que no cambian el significado.
- **Revisión de cumplimiento:** se realiza en las fases Plan y Review (sección 4).

## Fuentes

Fuentes consultadas el 2026-11-23. Inspiran esta constitution, pero no la sustituyen: lo que rige es lo que está escrito aquí, y cambiarlo requiere una enmienda (sección 6).

| Fuente | Qué se tomó de ella | Dónde se aplica |
| --- | --- | --- |
| [GitHub Spec Kit: constitution-template.md](https://raw.githubusercontent.com/github/spec-kit/main/templates/constitution-template.md) | Estructura: principios, secciones adicionales, Governance, versión y fechas. | Secciones 1 y 6 |
| [GitHub Spec Kit: spec-driven.md](https://raw.githubusercontent.com/github/spec-kit/main/spec-driven.md) | Constitution como conjunto de principios inmutables; proceso de enmienda con motivo, aprobación y evaluación de impacto. | Secciones 1 y 6 |
| [GitHub Spec Kit: commands/constitution.md](https://raw.githubusercontent.com/github/spec-kit/main/templates/commands/constitution.md) | Versionado semántico (MAJOR/MINOR/PATCH); principios declarativos y verificables, con justificación. | Secciones 1 y 6 |
| [GitHub Spec Kit: plan-template.md](https://raw.githubusercontent.com/github/spec-kit/main/templates/plan-template.md) y [commands/analyze.md](https://raw.githubusercontent.com/github/spec-kit/main/templates/commands/analyze.md) | Contraste del plan contra la constitution antes de avanzar; una violación es bloqueante y no se reinterpreta. | Sección 4 |
| [Claude Code: best practices](https://code.claude.com/docs/en/best-practices) | Mantener los archivos de contexto cortos y solo con lo que el agente no puede deducir. | Estilo general |

Decisiones propias de este repositorio, sin fuente externa: los cuatro gates humanos G1-G4, el ciclo con sus fases, los subagentes (con sus fases o su rol transversal, incluido `git_flow`), el reparto de precedencia con `AGENTS.MD`, y P6 (TDD estricto con stack documentado bajo `docs/decisions/`, sin fijar nombre de archivo ni runner en el harness).

**Enmienda 1.1.0 (2026-11-23):** se agrega P6 (TDD + obligación de stack/uso en un archivo bajo `docs/decisions/`; si falta, el agente lo exige al humano), reglas de Plan/Tasks/Implement ligadas a P6, y el bloque RESERVADO de producto pasa a numerar desde P7. Impacto: planes y tasks futuros deben citar la decisión de pruebas existente y desglosar comportamiento ejecutable en orden red→green→refactor; artefactos ya aprobados bajo 1.0.0 deben reabrirse si dejan de cumplir P6 (sección 6, P4).

**Enmienda 1.2.0 (2026-11-26):** se agrega el subagente transversal `git_flow` (sección 3) para ejecutar el proceso GitFlow (ramas, publicación, MRs) sin alterar el ciclo SDD ni los gates. Impacto: el `leader` (u otro agente) puede delegarle operaciones Git vía brief; hace falta su rol en `.agents/roles/git_flow.md`, plantillas de progreso y adaptador nativo. No reabre artefactos de fase ya aprobados.

**Enmienda 1.3.0 (2026-11-26):** se agrega en la sección 2 la mecánica «Ajustes pedidos por el humano durante el ciclo»: el agente principal deriva al `leader`, que decide qué fase reabrir (P4) y a qué subagente delegar, sin aplicar el cambio fuera del ciclo. Impacto: el rol `leader` documenta el disparador y el procedimiento; no reabre por sí sola artefactos ya aprobados (solo aplica cuando el humano pida un ajuste en un ciclo activo).

**Version**: 1.3.0 | **Ratified**: TODO(RATIFICATION_DATE): confirmar la fecha de adopción | **Last Amended**: 2026-11-26
