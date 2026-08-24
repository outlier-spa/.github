# Gobierno GitHub Outlier

Este repositorio centraliza los archivos organizacionales y los estandares de trabajo para los repositorios de `outlier-spa`.

> Este repositorio es publico. No agregar informacion confidencial, nombres de ambientes, secretos, credenciales, clientes sensibles, diagramas internos ni detalles de infraestructura privada.

## Proposito

El repositorio `.github` se usa para definir criterios comunes de trabajo en GitHub:

- perfil publico de la organizacion;
- templates de issues;
- template de pull request;
- guia de contribucion;
- guia de seguridad;
- flujo de backlog;
- estandar de labels;
- estandar de topics;
- estandar de nombres de repositorios;
- criterios para archivar o mantener repositorios;
- recomendaciones de ramas, permisos y revisiones.

## Archivos principales

| Archivo | Uso |
|---|---|
| `profile/README.md` | Perfil visible de la organizacion en GitHub. |
| `README.md` | Indice y proposito de este repositorio. |
| `GOVERNANCE.md` | Marco general de gobierno GitHub. |
| `CONTRIBUTING.md` | Guia para crear issues, ramas, commits y pull requests. |
| `.github/PULL_REQUEST_TEMPLATE.md` | Checklist comun para pull requests. |
| `SECURITY.md` | Politica base para reportar problemas de seguridad. |
| `SUPPORT.md` | Como pedir soporte o canalizar solicitudes. |
| `CODE_OF_CONDUCT.md` | Reglas basicas de convivencia y colaboracion. |
| `.github/CODEOWNERS` | Responsables de revision para este repositorio. |
| `.github/ISSUE_TEMPLATE/` | Formularios estandar para issues. |
| `.github/labels.yml` | Lista base de labels para sincronizacion posterior. |
| `docs/labels.md` | Estandar de etiquetas para issues y PRs. |
| `docs/topics.md` | Estandar de topics para clasificar repositorios. |
| `docs/repository-naming.md` | Estandar de nombres de repositorios. |
| `docs/repository-classification.md` | Criterios para clasificar repositorios. |
| `docs/repository-lifecycle.md` | Estados de ciclo de vida de repositorios. |
| `docs/repository-checklist.md` | Checklist minimo para repositorios activos. |
| `docs/repository-readme.md` | Estructura sugerida para README de proyectos. |
| `docs/backlog-workflow.md` | Flujo recomendado de backlog. |
| `docs/branching.md` | Ramas, pull requests y protecciones. |
| `docs/teams-permissions.md` | Recomendaciones de equipos y permisos. |
| `docs/codeowners.md` | Guia para definir responsables de revision por ruta. |

## Regla de oro

Cada repositorio activo debe poder responder rapidamente:

1. Que es este repositorio.
2. Quien lo mantiene.
3. Como se instala o ejecuta.
4. Como se despliega o publica.
5. Como se reportan bugs o tareas.
6. Cual es su estado: activo, mantenido, legacy, experimental o archivado.

## Implementacion recomendada

1. Mantener este repositorio como fuente de estandares.
2. Replicar labels en repos activos.
3. Agregar topics a todos los repositorios.
4. Completar README en repos activos y mantenidos.
5. Archivar repositorios obsoletos o sin uso.
6. Usar GitHub Projects para visibilidad transversal del backlog.
