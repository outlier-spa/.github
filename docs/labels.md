# Estandar de labels

Este documento define el set base de etiquetas para issues y pull requests en los repositorios de Outlier.

## Principios

- Usar prefijos para evitar labels ambiguas.
- Mantener el mismo set en repositorios activos.
- Evitar duplicados como `bug`, `bugs`, `error`, `fix`.
- Priorizar etiquetas que ayuden a filtrar backlog y responsabilidad.

## Tipo

| Label | Uso |
|---|---|
| `type: bug` | Error o comportamiento incorrecto. |
| `type: feature` | Nueva funcionalidad. |
| `type: task` | Actividad puntual tecnica u operativa. |
| `type: docs` | Documentacion. |
| `type: refactor` | Cambio interno sin cambio funcional esperado. |
| `type: chore` | Mantencion, configuracion o trabajo rutinario. |
| `type: technical-debt` | Deuda tecnica identificada. |
| `type: incident` | Problema operacional o productivo. |
| `type: question` | Duda o analisis pendiente. |

## Estado

| Label | Uso |
|---|---|
| `status: triage` | Requiere clasificacion inicial. |
| `status: ready` | Listo para tomar. |
| `status: in-progress` | En desarrollo o ejecucion. |
| `status: blocked` | Bloqueado por dependencia externa o decision. |
| `status: review` | En revision tecnica o funcional. |
| `status: waiting-client` | Esperando respuesta del cliente o usuario. |
| `status: waiting-data` | Esperando datos, archivos, accesos o informacion. |
| `status: done` | Terminado. |

## Prioridad

| Label | Uso |
|---|---|
| `priority: p0-critical` | Incidente critico, caida productiva o bloqueo mayor. |
| `priority: p1-high` | Alto impacto o compromiso cercano. |
| `priority: p2-medium` | Importante, pero no urgente. |
| `priority: p3-low` | Bajo impacto o mejora menor. |

## Area

| Label | Uso |
|---|---|
| `area: frontend` | Interfaz web o UI. |
| `area: backend` | API, servicios o logica servidor. |
| `area: database` | Base de datos, migraciones o consultas. |
| `area: collector` | Captura, integracion o sincronizacion de datos. |
| `area: mobile` | Aplicaciones moviles. |
| `area: infra` | Infraestructura, deployment, cloud o CI/CD. |
| `area: design` | Diseno UI/UX, componentes visuales o experiencia. |
| `area: docs` | Documentacion. |
| `area: security` | Seguridad, permisos, secretos o autenticacion. |
| `area: qa` | Pruebas y control de calidad. |
| `area: ai` | Automatizaciones o funciones basadas en IA. |

## Tamano

| Label | Uso |
|---|---|
| `size: xs` | Menos de medio dia. |
| `size: s` | Alrededor de 1 dia. |
| `size: m` | 2 a 3 dias. |
| `size: l` | 1 semana aproximada. |
| `size: xl` | Debe dividirse en issues menores. |

## Regla practica

Todo issue activo deberia tener, como minimo:

```text
type: ...
status: ...
priority: ...
area: ...
```

