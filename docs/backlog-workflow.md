# Flujo de backlog

Este documento define el flujo base para registrar, priorizar y ejecutar trabajo en GitHub.

## Principio general

Todo trabajo que requiera trazabilidad debe partir como issue. El issue debe vivir en el repositorio donde se realizara el cambio, y puede visualizarse en un GitHub Project central cuando aplique.

```text
Idea / solicitud -> Issue -> Triage -> Ready -> In progress -> Pull request -> Review -> Done
```

## Estados recomendados

| Estado | Uso |
|---|---|
| Inbox | Solicitud recibida, aun sin revisar. |
| Triage | Se esta validando alcance, prioridad, responsable y repositorio correcto. |
| Ready | Lista para tomar por el equipo. |
| In progress | En desarrollo, diseno, documentacion o analisis. |
| Review | Tiene pull request, evidencia o revision pendiente. |
| Blocked | Bloqueada por datos, acceso, definicion, cliente, proveedor o dependencia tecnica. |
| Done | Terminado y validado. |
| Archived | Cerrado por obsolescencia, duplicidad o decision de no ejecutar. |

## Reglas de uso

- Evitar registrar tareas solo en chats o correos si requieren seguimiento.
- Mantener un issue por unidad de trabajo clara.
- Dividir issues demasiado grandes en subtareas o issues relacionados.
- Vincular pull requests al issue correspondiente.
- Cerrar issues solo cuando exista evidencia suficiente de termino.
- No incluir secretos, tokens, credenciales ni informacion sensible en issues.

## Priorizacion

| Prioridad | Criterio |
|---|---|
| p0-critical | Interrumpe operacion critica, seguridad, datos productivos o disponibilidad. |
| p1-high | Bloquea entrega comprometida o afecta a usuarios clave. |
| p2-medium | Importante, pero existe alternativa temporal. |
| p3-low | Mejora, ajuste menor o deuda tecnica no urgente. |

## Campos sugeridos en GitHub Projects

- Status
- Priority
- Type
- Area
- Client
- Product
- Repository
- Owner
- Due date
- Quarter

## Criterio de cierre

Un issue puede cerrarse cuando:

- el cambio fue mergeado o la accion fue ejecutada;
- la correccion fue validada por quien corresponde;
- la documentacion o evidencia fue adjuntada si aplica;
- no quedan subtareas bloqueantes abiertas.
