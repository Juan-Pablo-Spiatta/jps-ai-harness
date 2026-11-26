# Convención: GitFlow

Este repositorio usa **GitFlow** para el trabajo con ramas. El subagente transversal que ejecuta este proceso es [`git_flow`](../../.agents/roles/git_flow.md).

En este documento, **MR** significa merge request o pull request, según el host del repositorio.

## Ramas permanentes

| Rama GitFlow | Nombre en este repo | Uso |
| --- | --- | --- |
| `master` | `main` | Releases |
| `develop` | `dev` | Integración del trabajo revisado |

Al inicializar GitFlow en un checkout nuevo, elegir expresamente `main` y `dev`. No aceptar `develop` como valor por defecto.

## Prefijos de ramas auxiliares

| Tipo | Prefijo | Origen habitual | Destino habitual del MR |
| --- | --- | --- | --- |
| Feature | `feature/` | `dev` | `dev` |
| Bugfix | `bugfix/` | `dev` | `dev` |
| Release | `release/` | `dev` | `main` (y luego también a `dev` vía MR) |
| Hotfix | `hotfix/` | `main` | `main` (y luego también a `dev` vía MR) |
| Support | `support/` | según el caso | según el caso |

## Reglas

- El trabajo de integración nace desde `origin/dev` (o con `git flow feature start …`, equivalente).
- Las ramas permanentes (`main`, `dev`) se actualizan solo mediante MRs. No hay push directo ni force push a ellas.
- Los MRs de trabajo cotidiano apuntan a **`dev`**, aunque el host sugiera `main` por ser la rama por defecto.
- Un release a `main` es otro MR; las correcciones que lleguen a `main` se incorporan también a `dev` mediante MR.
- `git flow … finish` no sustituye la revisión ni habilita push a ramas permanentes.
- Los agentes no crean tags de versión.
- Los agentes solo crean commits, hacen push o abren MRs cuando el humano lo autoriza de forma explícita.
- Los mensajes de commit no tienen un formato impuesto: deben ser claros y descriptivos, en el idioma que use el humano en el hilo, y sin secretos ni credenciales.

## Qué no hacer

- Tratar `main` como rama de integración diaria.
- Abrir MRs de feature/bugfix con destino `main` salvo hotfixes acordados.
- Force push o push directo a `main` o `dev`.
- Inventar prefijos de rama ajenos a la tabla anterior para trabajo nuevo.
