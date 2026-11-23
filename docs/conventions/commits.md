# Convención: mensajes de commit

Formato de mensajes de commit en este repositorio. Los agentes solo crean commits cuando el humano lo pide explícitamente; al hacerlo, siguen esta convención.

## Formato

```text
<tipo>(<ámbito opcional>): <descripción corta>

[cuerpo opcional]

[pie opcional]
```

- **tipo** (obligatorio): una de las palabras de la tabla siguiente, en minúsculas.
- **ámbito** (opcional): zona afectada en kebab-case o snake_case según el artefacto (`sdd`, `agents`, `docs`, `constitution`).
- **descripción**: imperativo, minúscula al inicio, sin punto final, ≤ ~72 caracteres en la primera línea.
- Idioma: el mismo que use el humano en el hilo (español o inglés); no mezclar en un mismo mensaje.

## Tipos

| Tipo | Cuándo |
| --- | --- |
| `feat` | Nueva capacidad o artefacto útil para el usuario del harness |
| `fix` | Corrección de un defecto |
| `docs` | Solo documentación (incl. `docs/conventions/`, plantillas, roles) |
| `refactor` | Cambio interno sin cambiar comportamiento observable |
| `chore` | Mantenimiento (ignore, metadatos, limpieza sin lógica) |
| `test` | Añadir o ajustar pruebas |
| `style` | Formato que no cambia significado (espacios, wrapping) |

## Ejemplos

```text
docs(conventions): add file-naming and commits conventions
```

```text
feat(sdd): add tasks template for phase breakdown
```

```text
fix(agents): correct spec_author output path in brief
```

## Qué no hacer

- Mensajes genéricos (`update`, `wip`, `fix stuff`).
- Varios temas no relacionados en un solo commit cuando se puedan separar.
- Incluir secretos, credenciales o dumps en el mensaje o en el diff del commit.
