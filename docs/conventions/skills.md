# Convención: skills

Las skills reutilizables del harness se mantienen en `.agents/skills/`. Esta
carpeta es la fuente compartida de verdad del contenido de cada skill,
independientemente del agente o de la herramienta con la que se ejecute.

## Estructura

Cada skill ocupa una carpeta propia cuyo nombre está en `kebab-case`:

```text
.agents/
  skills/
    <skill-slug>/
      SKILL.md
      references/   # opcional: documentación de apoyo
      scripts/      # opcional: automatizaciones auxiliares
      assets/       # opcional: recursos estáticos
```

Solo `SKILL.md` es obligatorio. Las subcarpetas opcionales se agregan
únicamente cuando la skill las necesita; no se crean vacías.

## `SKILL.md`

`SKILL.md` contiene las instrucciones completas y autosuficientes de la skill.
Como mínimo debe incluir:

1. **Propósito:** qué capacidad aporta.
2. **Cuándo usarla:** condiciones de activación y alcance.
3. **Procedimiento:** pasos que debe seguir el agente.
4. **Entradas y salidas:** información requerida y resultado esperado.
5. **Límites:** acciones fuera de alcance, riesgos y cuándo detenerse o
   preguntar al humano.
6. **Referencias:** rutas relativas a `references/`, `scripts/` o `assets/`,
   si existen.

La skill debe poder leerse sin depender del contexto de una herramienta
concreta. No debe duplicar `AGENTS.md`, `constitution.md` ni el contenido de
un rol; debe indicar cómo se relaciona con ellos cuando sea necesario.

Plantilla mínima:

```markdown
# Skill: <nombre>

## Propósito

<Qué capacidad aporta.>

## Cuándo usarla

<Cuándo se activa y cuál es su alcance.>

## Procedimiento

<Pasos verificables.>

## Entradas y salidas

<Qué necesita y qué produce.>

## Límites

<Cuándo detenerse, preguntar o no aplicarla.>
```

## Relación con agentes y herramientas

- `.agents/skills/<skill-slug>/SKILL.md` es la fuente única del contenido; no
  se mantienen copias por agente.
- Los adaptadores nativos de `.github/agents/`, `.claude/agents/`,
  `.cursor/agents/` o `.codex/agents/` solo deben declarar o referenciar una
  skill si la herramienta lo necesita para descubrirla o activarla.
- Si una herramienta exige otro formato de registro, ese archivo es un
  adaptador mínimo: no duplica las instrucciones de `SKILL.md`.
- La existencia de una skill en `.agents/skills/` no implica que todas las
  herramientas la descubran o la activen automáticamente. La compatibilidad
  y el mecanismo de activación deben verificarse en la documentación oficial
  de la herramienta antes de publicar un adaptador.
- Las skills no forman parte de las fases SDD ni sustituyen a los roles de
  `.agents/roles/`. Si una skill modifica un artefacto gobernado por SDD,
  sigue aplicando el ciclo, los responsables y los gates definidos en
  `constitution.md`.

## Fuera de alcance

Este harness no define skills concretas, su catálogo, sus prompts de
activación ni implementaciones auxiliares. Solo define su ubicación y forma
portable.
