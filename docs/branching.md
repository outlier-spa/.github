# Ramas y pull requests

Este documento define una convencion simple para ramas, pull requests y proteccion de ramas.

## Rama por defecto

Para repositorios nuevos, usar:

```text
main
```

Usar `prod`, `dev` o `develop` solo cuando exista una razon operacional clara y documentada en el README del repositorio.

## Nombres de ramas

Usar prefijos consistentes:

```text
feature/<descripcion-corta>
fix/<descripcion-corta>
task/<descripcion-corta>
docs/<descripcion-corta>
refactor/<descripcion-corta>
chore/<descripcion-corta>
hotfix/<descripcion-corta>
```

Ejemplos:

```text
feature/report-export
fix/calendar-date-shift
docs/update-readme
chore/update-dependencies
```

## Pull requests

Todo pull request debe incluir:

- resumen del cambio;
- issue relacionado, si existe;
- tipo de cambio;
- evidencia o capturas cuando aplique;
- riesgos y pasos de validacion;
- notas de despliegue si corresponde.

## Reglas recomendadas para repos activos

- Proteger `main` o `prod`.
- Evitar push directo a ramas protegidas.
- Requerir pull request antes de mergear.
- Requerir al menos una revision.
- Requerir checks de CI cuando existan.
- Eliminar ramas despues del merge.

## Reglas para repos criticos

Para repos de infraestructura, autenticacion, seguridad, datos o produccion:

- exigir revision de responsable tecnico;
- usar CODEOWNERS cuando los equipos esten definidos;
- exigir checks obligatorios;
- registrar riesgos de despliegue;
- evitar merges sin validacion.

## Estrategia de merge

Recomendacion general:

| Tipo | Estrategia sugerida |
|---|---|
| Feature o fix pequeno | Squash merge |
| Cambios con historial relevante | Merge commit |
| Librerias con historial lineal | Rebase merge si el equipo lo usa consistentemente |

## Hotfix

Un hotfix debe:

1. crear rama desde la rama productiva;
2. corregir solo el problema urgente;
3. incluir validacion minima;
4. hacer merge a produccion;
5. sincronizar el cambio con la rama de desarrollo si existe.
