# Gobierno de GitHub Outlier

Este documento define un marco simple para ordenar repositorios, issues, pull requests, permisos y documentacion dentro de la organizacion.

## Objetivo

Mantener GitHub como una fuente confiable para:

- encontrar repositorios activos;
- saber quien mantiene cada proyecto;
- registrar backlog y deuda tecnica;
- revisar cambios con trazabilidad;
- reducir repositorios obsoletos o ambiguos;
- proteger codigo, datos y configuraciones sensibles.

## Clasificacion de repositorios

Cada repositorio debe tener un estado definido:

```text
status-active
status-maintained
status-legacy
status-experiment
status-template
status-archive-candidate
status-delete-candidate
```

### status-active

Repositorio usado activamente en desarrollo, soporte, operacion o despliegue.

### status-maintained

Repositorio estable, con bajo cambio, pero aun soportado.

### status-legacy

Repositorio historico que podria contener codigo util o referencia operacional, pero no deberia recibir nuevas funcionalidades salvo excepcion.

### status-experiment

Repositorio de prueba, investigacion o prototipo. Debe tener fecha o criterio de revision.

### status-template

Repositorio usado como base para crear nuevos proyectos.

### status-archive-candidate

Repositorio que debe evaluarse para archivo.

### status-delete-candidate

Repositorio vacio, duplicado o sin valor historico aparente. Antes de eliminar, debe validarse con el responsable.

## Roles sugeridos

```text
owner
maintainer
developer
designer
external-collaborator
reader
```

- Owner: administra la organizacion y permisos globales.
- Maintainer: responsable tecnico de uno o mas repositorios.
- Developer: puede trabajar mediante branches y pull requests.
- Designer: puede participar en issues, documentacion y recursos visuales.
- External collaborator: acceso limitado a repositorios especificos.
- Reader: lectura controlada para revision o auditoria.

## Reglas minimas para repos activos

Todo repositorio activo debe tener:

- README actualizado;
- descripcion en GitHub;
- topics de clasificacion;
- responsable o equipo mantenedor;
- issues habilitados si se gestiona backlog en GitHub;
- branch principal definida;
- reglas de pull request si es critico;
- instrucciones de configuracion local;
- instrucciones de despliegue o publicacion si aplica.

## Reglas para archivar repositorios

Antes de archivar:

1. Validar que no se use en produccion.
2. Cerrar o migrar issues vigentes.
3. Cerrar pull requests obsoletos.
4. Actualizar README indicando estado y repositorio reemplazante si existe.
5. Quitar automatizaciones innecesarias.
6. Reducir permisos si corresponde.
7. Archivar el repositorio.

## Reglas para repos publicos

Todo repositorio publico debe revisarse con mayor cuidado:

- no debe contener secretos;
- no debe exponer datos de clientes;
- no debe contener configuraciones productivas sensibles;
- debe tener README claro;
- debe tener licencia solo si corresponde;
- debe tener SECURITY.md o heredar el de la organizacion.

## Revision periodica

Se recomienda una revision trimestral de:

- repositorios sin actividad;
- repositorios sin README;
- repositorios sin descripcion;
- repositorios con ramas por defecto no estandar;
- pull requests antiguos;
- issues antiguos sin estado;
- permisos por usuario directo;
- repositorios publicos.
