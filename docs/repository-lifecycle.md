# Ciclo de vida de repositorios

Este documento define estados sugeridos para clasificar repositorios y reducir ruido operacional.

## Estados

| Estado | Uso |
|---|---|
| `status-active` | Repositorio con desarrollo activo. |
| `status-maintained` | Repositorio estable, con mantencion ocasional. |
| `status-legacy` | Repositorio antiguo, aun necesario, pero no recomendado para nuevo desarrollo. |
| `status-experiment` | Prueba, POC o investigacion. |
| `status-template` | Plantilla para crear nuevos repositorios. |
| `status-archive-candidate` | Candidato a archivar. |
| `status-delete-candidate` | Candidato a eliminar, si no tiene valor historico. |
| `archived` | Repositorio archivado en GitHub. |

## Criterios para repositorio activo

Un repositorio activo debe tener:

- README actualizado;
- responsable o equipo mantenedor;
- rama principal clara;
- backlog o issues vigentes;
- criterios de build/test/run;
- descripcion y topics;
- proteccion de ramas si es critico.

## Criterios para repositorio legacy

Un repositorio legacy debe tener README con:

- razon de legado;
- si aun se usa en produccion;
- repositorio reemplazante si existe;
- advertencias de mantenimiento;
- responsable minimo.

## Criterios para archivar

Un repositorio puede archivarse si:

- no tiene desarrollo activo;
- no se usa en produccion;
- fue reemplazado por otro repositorio;
- solo se mantiene por historia;
- sus issues fueron cerrados o migrados;
- no existen PRs relevantes abiertos.

Antes de archivar:

1. Revisar issues abiertos.
2. Cerrar o migrar issues vigentes.
3. Cerrar PRs obsoletos.
4. Actualizar README con estado final.
5. Indicar repositorio reemplazante si aplica.
6. Reducir permisos si corresponde.
7. Archivar desde GitHub.

## Candidatos a eliminar

Eliminar solo si:

- no contiene codigo util;
- no tiene historia relevante;
- no contiene documentacion valiosa;
- no existe dependencia externa;
- hay respaldo o confirmacion del responsable.

## README minimo para repositorios archivados

```markdown
# Nombre del repositorio

Estado: archivado

Este repositorio ya no recibe mantenimiento activo.

Motivo:
- Reemplazado por: <repo>
- Fecha de archivo: YYYY-MM-DD
- Responsable historico: <equipo>

No crear issues ni pull requests nuevos en este repositorio.
```

