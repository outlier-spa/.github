# Estandar de nombres de repositorios

El objetivo del estandar es que el nombre de un repositorio indique rapidamente su contexto, producto y tipo tecnico.

## Regla general

Usar `kebab-case`:

```text
minusculas-con-guiones
```

Evitar:

```text
Mayusculas
snake_case
Puntos.En.El.Nombre
nombres genericos
nombres temporales
```

## Patrones recomendados

### Proyectos de cliente o producto

```text
<cliente>-<producto>-<modulo>
```

Ejemplos:

```text
cliente-producto-api
cliente-producto-frontend
cliente-producto-collector
cliente-producto-mobile
cliente-producto-docs
```

### Componentes reutilizables

```text
component-<nombre>
```

Ejemplos:

```text
component-table
component-chart
component-theme
component-date-picker
component-editor
```

### Librerias internas

```text
lib-<nombre>
```

Ejemplos:

```text
lib-json
lib-excel
lib-geometry
lib-cache
lib-email
```

### Herramientas internas

```text
tool-<nombre>
```

Ejemplos:

```text
tool-github-notifier
tool-deployment
tool-file-cleaner
```

### Templates

```text
template-<tecnologia>-<tipo>
```

Ejemplos:

```text
template-dotnet-api
template-dotnet-library
template-react-component
template-web-app
```

## Nombres a evitar

Evitar nombres que no expliquen el contenido:

```text
test
main
admin
core
data
helper
temp
asd
hola
```

Si se requiere un repositorio temporal, agregar prefijo y fecha o contexto:

```text
experiment-ai-agent-2026
sandbox-github-actions
poc-visualizer-map
```

## Renombrar repos existentes

No renombrar repositorios activos sin evaluar impacto. Antes de renombrar, validar:

- dependencias NuGet/npm;
- pipelines;
- submodulos;
- links en documentacion;
- webhooks;
- permisos;
- referencias desde otros repositorios;
- scripts de despliegue.

## Descripcion del repositorio

Todo repositorio activo debe tener una descripcion breve:

```text
API para gestion de reportes operacionales.
Componente React para tablas editables.
Collector para sincronizacion de datos operacionales.
```

## Topics recomendados

Usar topics para clasificar sin renombrar inmediatamente:

```text
type-api
type-frontend
type-component
type-library
type-collector
type-infra
type-docs
status-active
status-maintained
status-legacy
status-experiment
client-internal
product-imp
```

