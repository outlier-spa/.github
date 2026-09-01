# GitHub Repository Standards

**Versión:** 1.0  
**Estado:** Propuesta base  
**Alcance:** todos los repositorios de la organización `outlier-spa`.

## 1. Propósito

Este estándar define cómo crear, nombrar, documentar y mantener los repositorios de Outlier. Su objetivo es que una persona pueda identificar el propósito, responsable, tecnología y estado operativo de un repositorio sin depender del conocimiento de quien lo creó.

## 2. Principios

1. Un repositorio representa una unidad clara de producto, servicio, librería, plantilla o configuración organizacional.
2. Los nombres son estables, comprensibles y no dependen de una persona, cargo o fecha.
3. La documentación inicial permite instalar, ejecutar, probar y contribuir.
4. Issues y pull requests son trazables mediante un catálogo común de labels.
5. Los repositorios privados protegen código, datos de clientes, configuraciones y propiedad intelectual de Outlier.

## 3. Nombre del repositorio

### 3.1 Regla general

- Los nombres usan **kebab-case**, solo con letras minúsculas, números y guiones.
- Los repositorios deben terminar con un sufijo permitido y el sufijo es obligatorio, salvo las excepciones de nombres reservados como `.github`.
- No se usan espacios, mayúsculas, guiones bajos, fechas, versiones, nombres de personas ni nombres ambiguos como `test`, `nuevo` o `final`.
- El nombre describe el producto o responsabilidad; no la tecnología, salvo en plantillas o herramientas técnicas donde sea necesaria para distinguirlo.
- Los repositorios existentes como `dataset`, `dateutils` y `component` no requieren renombrarse. Esta regla guía los nuevos repositorios.

Los sufijos permitidos son: `-library`, `-package`, `-console`, `-api`, `-service`, `-model`, `-deliverer`, `-helper`, `-agent`, `-collector`, `-crafter`, `-web`, `-app`, `-infra`, `-tool`, `-template` y `-docs`.

### 3.2 Patrones aprobados

| Tipo | Patrón | Ejemplo |
| --- | --- | --- |
| Solución de cliente | `<cliente>-<producto>-<tipo>` | `bhp-imp-api` |
| Plataforma o producto interno | `<producto>-<tipo>` | `dataset-service` |
| Librería compartida | `<capacidad>-library` | `geometry-library` |
| Plantilla | `<tecnología>-template` | `dotnet-template` |
| Herramienta interna | `<capacidad>-tool` | `repository-tool` |
| Configuración organizacional | nombre reservado | `.github` |

Si un producto incluye varios repositorios, se conserva un prefijo común: `bhp-imp-api`, `bhp-imp-collector` y `bhp-imp-web`.

### 3.3 Tecnología y tipo de repositorio

La organización puede mantener repositorios escritos en **C#** y **TypeScript**. Todo repositorio declara su tecnología principal, tipo y propósito en la descripción de GitHub y en el README. La tecnología no reemplaza al tipo: por ejemplo, un repositorio puede ser una `api` de C# o una `api` de TypeScript.

En repositorios C#, el tipo `library` se reserva para proyectos que generan paquetes NuGet reutilizables por otros proyectos C#. Estos repositorios deben usar el sufijo `-library`, por ejemplo `geometry-library`.

En repositorios TypeScript, el tipo `package` se reserva para proyectos que generan paquetes reutilizables, normalmente publicados o consumidos mediante npm. Estos repositorios deben usar el sufijo `-package`, por ejemplo `geometry-package`.

| Tipo | Propósito | Sufijo o patrón permitido | Ejemplo |
| --- | --- | --- | --- |
| `library` | Proyecto C# que genera un paquete NuGet reutilizable por otros proyectos C#. | `-library` obligatorio. | `geometry-library` |
| `package` | Proyecto TypeScript que genera un paquete reutilizable, normalmente para npm. | `-package` obligatorio. | `geometry-package` |
| `console` | Aplicación de consola desarrollada en C#. | `-console` | `data-import-console` |
| `api` | Backend expuesto mediante HTTP. | `-api` | `imp-api` |
| `service` | Worker o proceso backend sin API pública principal. | `-service` | `imp-notification-service` |
| `model` | Proyecto que contiene modelos, contratos o estructuras de datos compartidas. | `-model` | `geometry-model` |
| `deliverer` | Proceso que entrega o publica datos, resultados o mensajes hacia un destino. | `-deliverer` | `report-deliverer` |
| `helper` | Herramienta o componente de apoyo para una tarea específica. | `-helper` | `migration-helper` |
| `agent` | Proceso automatizado que ejecuta tareas o interactúa con otros sistemas. | `-agent` | `monitoring-agent` |
| `collector` | Captura e ingesta datos desde fuentes externas. | `-collector` | `spence-collector` |
| `crafter` | Proceso que construye, transforma o genera artefactos, datos o contenido. | `-crafter` | `schema-crafter` |
| `web` | Aplicación frontend. | `-web` | `imp-web` |
| `application` | Aplicación de escritorio o ejecutable para usuarios. | `-app` | `imp-app` |
| `infrastructure` | Infraestructura, CI/CD o configuración de despliegue. | `-infra` | `imp-infra` |
| `tool` | Herramienta interna de soporte o automatización. | `-tool` | `repository-tool` |
| `template` | Base reutilizable para crear repositorios. | `-template` | `dotnet-template` |
| `documentation` | Documentación o estándares organizacionales. | `-docs` | `platform-docs` |

Reglas:

- El nombre de todo repositorio debe incluir uno de los sufijos permitidos, salvo que exista una excepción aprobada para un repositorio legado o que use un nombre reservado como `.github`.
- No se agregan sufijos redundantes ni se combinan tipos sin justificación: `imp-backend-api` y `dataset-nuget-library` no son válidos.
- Si un producto tiene varias partes, se conserva un prefijo común: `imp-api`, `imp-web` e `imp-collector`.
- El tipo define requisitos adicionales de documentación y pipeline. Una `library` publica paquetes NuGet y una `package` publica paquetes TypeScript; una `api`, `service`, `deliverer`, `agent`, `collector`, `crafter`, `web` o `console` debe definir su ejecución, despliegue y monitoreo cuando corresponda.

## 4. Propiedad, visibilidad y ciclo de vida

- Todo repositorio se crea dentro de `outlier-spa`, no en cuentas personales.
- La visibilidad predeterminada es **private**. Un repositorio se hace público solo con una decisión explícita de la organización.
- Cada repositorio tiene al menos dos personas o un equipo con permisos de administración/mantenimiento para evitar dependencias de una sola persona.
- Todo repositorio tiene una descripción breve en GitHub y, cuando aporte descubrimiento, topics correctos.
- Los repositorios sin uso se archivan; no se eliminan salvo que su contenido sea obsoleto, recuperable y la eliminación esté aprobada.
- Los secretos no se guardan en el código, README, issues, variables de ejemplo ni archivos de configuración. Se usan GitHub Secrets, variables de entorno y archivos `.example` sin valores reales.

## 5. Contenido mínimo

Todo repositorio activo contiene:

```text
README.md
.gitignore
LICENSE                           # cuando aplique
.editorconfig                     # en repositorios .NET
.github/
  workflows/                      # cuando exista integración continua
docs/                             # cuando exista documentación técnica relevante
```

El `README.md` incluye, como mínimo:

1. Propósito y alcance del repositorio.
2. Estado del proyecto (activo, mantenimiento, experimental o archivado).
3. Requisitos y pasos mínimos para instalar, ejecutar y probar.
4. Dependencias o servicios externos necesarios.
5. Forma de publicar o desplegar, cuando corresponda.
6. Enlace a documentación adicional, estándares y forma de reportar trabajo.

Para librerías NuGet se agrega el nombre del paquete, frameworks soportados, instalación, ejemplo de uso y política de compatibilidad.

## 6. Topics

Los topics sirven para descubrir repositorios; no sustituyen la descripción ni los labels. Se usan en inglés, minúsculas y sin duplicar información.

Ejemplos por tipo:

| Repositorio | Topics recomendados |
| --- | --- |
| Librería C# publicada | `csharp`, `dotnet`, `nuget`, `library` |
| API | `csharp`, `dotnet`, `api` |
| Collector | `csharp`, `dotnet`, `collector`, `mining` cuando corresponda |
| Frontend | `frontend`, `web`, tecnología principal |
| Solución BHP / IMP | `bhp`, `imp`, tecnología principal |
| Plantilla | `template`, tecnología principal |

Se usan entre 3 y 6 topics. No se agregan topics de clientes cuando ello revele información que no deba ser pública.

## 7. Ramas, ambientes y pull requests

Todo repositorio activo mantiene estas ramas permanentes, salvo la excepción indicada en la sección 7.4:

```text
feature/* → dev → qa → prod
```

| Rama | Ambiente | Propósito | Origen permitido para PR |
| --- | --- | --- | --- |
| `dev` | Desarrollo | Integración continua de funcionalidades y pruebas internas. | `feature/*`, `fix/*`, `docs/*`, `refactor/*`, `chore/*` |
| `qa` | QA | Validación funcional, técnica y de aceptación. | `dev` |
| `prod` | Producción | Versión estable, aprobada y desplegable a producción. | `qa` |

- `dev` es la rama predeterminada de GitHub y el punto de integración inicial para el trabajo diario. `prod` representa la versión estable del repositorio.
- En repositorios desplegables (`api`, `service`, `collector`, `web` y `application`), cada rama permanente despliega automáticamente a su ambiente equivalente: `dev` a Desarrollo, `qa` a QA y `prod` a Producción.
- En librerías (`library`), las ramas siguen el mismo flujo de validación, pero publican o validan paquetes en canales equivalentes en lugar de desplegar un ambiente de ejecución.
- El trabajo se realiza en ramas cortas; patrón obligatorio: `<tipo>/<issue>-<descripcion>`.
- Tipos de rama: `feature/`, `fix/`, `docs/`, `refactor/`, `chore/` y `hotfix/`.
- Ejemplos: `feature/124-excel-import`, `fix/215-null-column`, `docs/31-update-readme`.
- Un pull request describe qué cambia, por qué, cómo se probó y qué impacto tiene para consumidores o despliegues.
- Las ramas de trabajo se eliminan después de integrar el PR. Solo `dev`, `qa` y `prod` permanecen de forma continua.

### 7.1 Hotfixes

Un `hotfix/*` se crea desde `prod` únicamente para corregir una incidencia crítica de producción. Se integra mediante PR a `prod` y luego se propaga mediante PR hacia `qa` y `dev`, para evitar que los ambientes vuelvan a divergir.

### 7.2 Protección obligatoria de ramas

Las ramas `dev`, `qa` y `prod` se protegen mediante una regla de protección o ruleset de GitHub. En todos los casos se prohíben los pushes directos, force pushes y la eliminación de la rama.

| Regla | `dev` | `qa` | `prod` |
| --- | --- | --- | --- |
| Pull request obligatorio | Sí | Sí | Sí |
| Aprobaciones mínimas | 1 | 1 | 1 |
| Origen esperado del PR | Rama de trabajo | `dev` | `qa` |
| Checks de CI obligatorios | Build y tests | Build, tests y despliegue a QA | Build, tests y despliegue a Producción |
| Rama actualizada antes de merge | Recomendado | Sí | Sí |
| Conversaciones resueltas | Sí | Sí | Sí |
| Descartar aprobación al recibir nuevos commits | Sí | Sí | Sí |
| Force push y eliminación | Prohibidos | Prohibidos | Prohibidos |
| Bypass para administradores | No | No | No |

La aprobación debe venir de una persona distinta de quien creó el último cambio del PR. En un caso de emergencia operacional, un administrador puede modificar temporalmente la regla, documentar el motivo en el PR o issue y restaurarla al finalizar.

### 7.3 Configuración en GitHub

Para proteger una rama, un administrador del repositorio debe ir a **Settings → Branches → Add rule** —o crear un ruleset equivalente en **Settings → Rules**— e indicar el nombre exacto de la rama: `dev`, `qa` o `prod`.

Se habilitan estas opciones:

1. **Require a pull request before merging**, con una aprobación mínima.
2. **Dismiss stale pull request approvals when new commits are pushed**.
3. **Require approval of the most recent reviewable push**.
4. **Require status checks to pass before merging** y seleccionar los checks del pipeline correspondiente.
5. **Require branches to be up to date before merging** para `qa` y `prod`.
6. **Require conversation resolution before merging**.
7. **Do not allow bypassing the above settings**.
8. Mantener deshabilitados **Allow force pushes** y **Allow deletions**.

GitHub protege el destino del PR, pero no restringe por sí solo que el origen sea `dev` o `qa`. El pipeline debe validar ese flujo: permitir solo `dev → qa` y `qa → prod`; cualquier otro origen debe fallar la validación.

### 7.4 Excepción para el repositorio `.github`

El repositorio organizacional `.github` contiene estándares, perfiles y configuración compartida de GitHub; no representa una aplicación, servicio, librería ni ambiente desplegable. Por lo tanto, mantiene únicamente la rama permanente `main`.

- `main` es la rama predeterminada y protegida de `.github`.
- Los cambios se realizan en ramas cortas y se integran mediante pull request hacia `main`.
- `.github` no requiere las ramas permanentes `dev`, `qa` ni `prod`.
- Las reglas de despliegue por ambiente no aplican a este repositorio.

## 8. Issues

- Los issues representan trabajo concreto: defecto, mejora, tarea técnica, documentación o seguridad.
- El título sigue el patrón: `<tipo>: <resultado esperado>`; por ejemplo `bug: avoid null values during CSV import`.
- Un issue describe contexto, resultado esperado, alcance, criterios de aceptación y, si corresponde, evidencia o pasos de reproducción.
- Un issue nuevo recibe `status: needs-triage` hasta que sea revisado.
- Las tareas grandes se dividen en issues que puedan revisarse y cerrarse de forma independiente.

## 9. Catálogo oficial de labels

Los labels se nombran en inglés, en minúsculas y con el prefijo de su categoría. Esto permite filtrar transversalmente sin depender del idioma del repositorio.

### 9.1 Labels obligatorios

| Label | Color | Uso |
| --- | --- | --- |
| `type: bug` | `d73a4a` | Comportamiento incorrecto respecto de lo esperado. |
| `type: feature` | `1d76db` | Nueva capacidad visible para usuarios o consumidores. |
| `type: enhancement` | `a2eeef` | Mejora de una capacidad existente. |
| `type: refactor` | `fbca04` | Mejora interna sin cambio funcional intencional. |
| `type: documentation` | `0075ca` | Documentación, ejemplos o comentarios de API. |
| `type: maintenance` | `c5def5` | Dependencias, build, CI, configuración o mantenimiento rutinario. |
| `type: security` | `b60205` | Vulnerabilidad, riesgo o endurecimiento de seguridad. |
| `priority: critical` | `b60205` | Riesgo operacional, seguridad o bloqueo que exige atención inmediata. |
| `priority: high` | `d93f0b` | Debe resolverse en el ciclo de trabajo actual. |
| `priority: medium` | `fbca04` | Importante, pero puede planificarse. |
| `priority: low` | `0e8a16` | Útil, sin urgencia ni impacto relevante. |
| `status: needs-triage` | `ededed` | Aún no revisado ni priorizado. |
| `status: ready` | `0e8a16` | Definido y disponible para ser tomado. |
| `status: in-progress` | `1d76db` | Trabajo activo. |
| `status: blocked` | `b60205` | No puede avanzar por una dependencia, decisión o acceso externo. |
| `status: needs-information` | `d876e3` | Faltan antecedentes para estimar o implementar. |
| `status: needs-review` | `5319e7` | Pull request o propuesta lista para revisión. |

### 9.2 Labels opcionales

| Label | Color | Uso |
| --- | --- | --- |
| `good first issue` | `7057ff` | Tarea acotada apta para una primera contribución. |
| `help wanted` | `008672` | Requiere apoyo adicional. |
| `breaking-change` | `b60205` | Cambia un contrato público o exige migración. |
| `duplicate` | `cfd3d7` | Repite un issue o PR existente. |
| `invalid` | `e4e669` | No corresponde a trabajo accionable. |
| `wontfix` | `ffffff` | Se decidió no implementar. |

### 9.3 Labels de área

Los labels `area:` son opcionales y se crean solo cuando un repositorio tiene suficiente complejidad. Ejemplos: `area: api`, `area: core`, `area: serialization`, `area: excel`, `area: collector`, `area: database`, `area: ci`.

No se usa un label por cada clase, pantalla o persona. Si un área deja de tener uso recurrente, se elimina o consolida.

### 9.4 Reglas de uso

- Todo issue abierto debe tener exactamente un label `type:` y un label `priority:`.
- Todo issue abierto debe tener a lo más un label `status:`.
- Los pull requests pueden usar `type:` y `status: needs-review`; no necesitan prioridad salvo que sea relevante.
- La asignación de persona, milestone y project no se reemplaza con labels.
- No se crean sinónimos como `bug`, `bugs`, `defect`, `error` o `urgent`; se usa el catálogo oficial.

## 10. Automatización y aplicación

GitHub mantiene labels por repositorio. El repositorio `.github` contiene este estándar como fuente de verdad, pero no replica los labels por sí solo.

La aplicación se realiza en dos etapas:

1. Crear el catálogo obligatorio en cada repositorio activo.
2. Incorporar una automatización o configuración central que sincronice los labels, después de validar el catálogo en algunos repositorios piloto.

No se eliminan labels existentes sin revisar su uso histórico y acordar la migración hacia el catálogo oficial.

## 11. Lista de verificación para crear un repositorio

- [ ] El nombre cumple el patrón y expresa una responsabilidad clara.
- [ ] El repositorio se creó en `outlier-spa` y con visibilidad correcta.
- [ ] Existe una descripción y entre 3 y 6 topics pertinentes.
- [ ] El README permite entender, instalar y probar el proyecto.
- [ ] Se configuraron `.gitignore`, `.editorconfig` y CI cuando corresponda.
- [ ] En repositorios con flujo por ambientes, `dev`, `qa` y `prod` están protegidas, y `dev` está configurada como rama predeterminada; en `.github`, solo `main` está protegida y configurada como rama predeterminada.
- [ ] Se creó el catálogo obligatorio de labels.
- [ ] Hay más de una persona o equipo responsable del repositorio.
- [ ] Los secretos y datos de clientes no están versionados.
