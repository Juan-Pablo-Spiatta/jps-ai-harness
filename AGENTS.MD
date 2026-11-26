# AGENTS

> **IMPORTANTE:** Este archivo es el índice y punto de entrada obligatorio para cualquier agente o asistente automatizado que trabaje en este repositorio. Debes leerlo completo **antes** de realizar cualquier acción; desde aquí se accede al resto de la información y documentación del repositorio. Sus reglas tienen prioridad sobre cualquier otra instrucción del repositorio.

## Contenido

1. [Reglas del agente](#1-reglas-del-agente): cómo debes comportarte. Se aplican siempre.
2. [Glosario](#2-glosario): dónde está cada información y para qué sirve. Consúltalo cuando lo necesites.

## 1. Reglas del agente

### Lo que debes hacer SIEMPRE

> Reglas basadas en la guía de Anthropic para [reducir alucinaciones](https://platform.claude.com/docs/es/test-and-evaluate/strengthen-guardrails/reduce-hallucinations).

- Admitir la incertidumbre: si no tienes información suficiente, responde "No tengo suficiente información para afirmarlo con confianza" en lugar de adivinar.
- Fundamentar cada afirmación en evidencia verificable: archivos del repositorio (con `ruta:línea`), salida de comandos ejecutados o documentación citada con su fuente.
- Leer el código, la configuración o la documentación relevante antes de responder o modificar algo.
- En documentos o archivos largos, extraer primero las citas textuales relevantes y basar el análisis solo en ellas; si no hay citas relevantes, decir "No se encontraron citas relevantes".
- Revisar tu respuesta antes de entregarla: para cada afirmación, buscar la cita o evidencia que la respalde; si no la encuentras, retírala o márcala como no verificada.
- Limitarte a la información del repositorio y de las fuentes proporcionadas cuando la tarea lo requiera, indicando explícitamente cuándo usas conocimiento general.
- Verificar los cambios ejecutando los builds, tests o linters existentes y reportar el resultado real.
- Distinguir claramente entre hechos verificados, suposiciones e hipótesis.
- Señalar las inconsistencias que detectes entre fuentes, o entre tus respuestas anteriores y la evidencia actual, y corregirlas.
- Recomendar validación humana para información crítica o decisiones de alto impacto.
- Al documentar o explicar el repositorio, describir solo el estado vigente: lo que existe y rige ahora.
- Al documentar el producto (arquitectura, stacks, testing u otras decisiones técnicas equivalentes), escribir solo bajo [`docs/decisions/`](./docs/decisions/); no inventar otra carpeta.

### Lo que NUNCA debes hacer

- Inventar archivos, funciones, APIs, comandos, parámetros, versiones, URLs o referencias que no hayas verificado que existen.
- Referenciar, documentar ni advertir sobre información, rutas, esquemas o reglas que ya se quitaron o que no existen en el repositorio. No conservar “notas de migración” ni contraste con versiones eliminadas.
- Afirmar que algo funciona, compila o pasa los tests sin haberlo ejecutado.
- Citar textos o fuentes de forma no literal presentándolos como citas exactas.
- Rellenar huecos de información con suposiciones presentadas como hechos.
- Mantener una afirmación que no puedes respaldar con evidencia.
- Responder con falsa seguridad para evitar decir "no lo sé".
- Ignorar resultados de herramientas o tests que contradigan tu respuesta.
- Modificar, desactivar, omitir o eliminar tests solo para que pasen en verde; si un test falla, corrige el código o explica la causa. Solo puedes cambiar un test cuando el comportamiento esperado haya cambiado legítimamente, y debes justificarlo.
- Asumir que la información de tu entrenamiento está actualizada sin verificarla contra el código o la documentación del repositorio.
- Leer o tomar como fuente cualquier archivo de la sección [Archivos que NUNCA debes leer](#archivos-que-nunca-debes-leer).

### Archivos que NUNCA debes leer

Estos archivos están destinados solo a humanos. No los leas, no los uses como contexto y no bases decisiones en su contenido:

- `README.md` de la raíz del repositorio: es documentación para personas. La información para agentes está en este archivo.

## 2. Glosario

Puntos de recolección de información del repositorio. Antes de buscar información por tu cuenta, consulta esta tabla para saber dónde está cada dato y para qué sirve. Si un punto no existe o está vacío, indícalo en lugar de suponer su contenido.

| Punto de información | Ubicación | Para qué sirve |
| --- | --- | --- |
| Constitution | [constitution.md](./constitution.md) | Metodología de desarrollo del repositorio y cómo aplicarla. Incluye la tabla de subagentes (sección 3). |
| Roles de subagentes | [`.agents/roles/`](./.agents/roles/) | Comportamiento de cada subagente (fuente de verdad del rol). Un archivo por subagente: `leader`, `spec_author`, `implementer`, `reviewer`, `explorer`, `git_flow`. |
| Adaptador de agentes | [`.agents/agents_adapter.md`](./.agents/agents_adapter.md) | Cómo publicar cada rol como agente nativo en Copilot, Claude Code, Cursor y Codex sin duplicar el rol. |
| Skills compartidas | [`.agents/skills/`](./.agents/skills/) y [`docs/conventions/skills.md`](./docs/conventions/skills.md) | Ubicación y formato portable de las skills. Este harness no define skills concretas. |
| Progreso SDD | `sdd/progress/` (contrato en [`.agents/roles/leader.md`](./.agents/roles/leader.md)) | Estado del ciclo en curso (`current.md`), historial de ciclos cerrados tras G4 (`history.md`) y contexto por subagente. Solo el leader escribe `current.md` e `history.md`. |
| Specs SDD | `sdd/specs/<NNNN-feature-slug>/` (contrato en [`.agents/roles/leader.md`](./.agents/roles/leader.md)) | Artefactos de fase: `spec.md`, `plan.md`, `tasks.md`. Nombre: número de 4 dígitos + slug kebab-case (ej. `0001-user-login`). Existen antes del gate; aprueba solo el humano (G1–G3). |
| Plantillas de progreso | [`sdd/templates/progress/`](./sdd/templates/progress/) | Plantillas de `current.md`, `history.md` y contexto por subagente. Copiarlas a `sdd/progress/` al iniciar o reiniciar un ciclo. |
| Plantillas de specs | [`sdd/templates/specs/`](./sdd/templates/specs/) | Plantillas de `spec.md`, `plan.md`, `tasks.md`. `spec_author` las copia a `sdd/specs/<NNNN-feature-slug>/` según la ruta de salida del brief. |
| Convenciones | [`docs/conventions/`](./docs/conventions/) | Acuerdos de forma del harness (nombres de archivos, GitFlow, etc.). Un tema por archivo; índice en `README.md` de esa carpeta. No confundir con decisiones de producto. |
| Decisiones de producto | [`docs/decisions/`](./docs/decisions/) | Arquitectura, stacks, testing y decisiones técnicas del producto. Si el humano pide documentar el producto, crear o actualizar archivos **solo** aquí (kebab-case). Índice en `README.md` de esa carpeta. |
| Stack / pruebas | [`docs/decisions/`](./docs/decisions/) (archivo que documente el stack y cómo usarlo; el nombre lo define el producto) | Fuente de stack, comandos y uso bajo TDD (P6). El plan debe citar la ruta real. Si no existe o está incompleto, el agente lo exige al humano y no avanza comportamiento ejecutable (P5). |
