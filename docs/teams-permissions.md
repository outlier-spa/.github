# Equipos y permisos

Esta guia propone una estructura simple para gestionar accesos en la organizacion `outlier-spa`.

## Principio general

Los permisos deben asignarse mediante equipos de GitHub, no usuario por usuario, salvo excepciones justificadas.

```text
Usuario -> Equipo -> Repositorios -> Permiso
```

## Equipos sugeridos

```text
owners
maintainers-platform
maintainers-imp
developers-imp
developers-components
developers-infra
developers-data
design-3d
external-collaborators
clients-readonly
```

## Niveles de permiso

| Permiso | Uso recomendado |
|---|---|
| Read | Lectura y revision. |
| Triage | Gestionar issues sin modificar codigo. |
| Write | Desarrollo mediante branches y PRs. |
| Maintain | Gestion operativa del repositorio sin permisos globales. |
| Admin | Solo owners o responsables criticos. |

## Reglas base

- Minimizar accesos `Admin`.
- Usar `Maintain` para responsables tecnicos.
- Usar `Write` para desarrollo diario.
- Usar `Triage` para equipos que gestionan backlog sin tocar codigo.
- Revisar colaboradores externos periodicamente.
- Eliminar accesos directos que puedan representarse con equipos.

## Repos criticos

Repositorios de infraestructura, autenticacion, datos, seguridad o despliegue deben tener permisos mas restrictivos.

Recomendaciones:

- rama principal protegida;
- revision obligatoria;
- CODEOWNERS cuando existan equipos definidos;
- acceso Admin muy limitado;
- revision periodica de colaboradores externos.

## Colaboradores externos

Los colaboradores externos deben tener acceso solo a los repositorios necesarios para su trabajo.

Checklist:

- [ ] Tiene repositorio asignado.
- [ ] Tiene permiso minimo suficiente.
- [ ] Tiene fecha o condicion de revision.
- [ ] No tiene acceso a repositorios sensibles innecesarios.
- [ ] No tiene acceso Admin salvo excepcion documentada.

## Revision periodica

Frecuencia recomendada: trimestral.

Revisar:

- usuarios sin actividad;
- permisos Admin;
- accesos directos fuera de equipos;
- colaboradores externos;
- repositorios publicos;
- repositorios archivados con permisos innecesarios.
