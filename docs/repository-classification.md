# Clasificacion de repositorios

La clasificacion ayuda a ordenar la organizacion sin renombrar todo de inmediato.

## Estado del repositorio

Usar estos estados como topics o en la descripcion del repo:

```text
status-active
status-maintained
status-legacy
status-experiment
status-template
status-archive-candidate
status-delete-candidate
```

## Tipo tecnico

```text
type-app
type-api
type-frontend
type-mobile
type-collector
type-component
type-library
type-tool
type-template
type-docs
type-infra
type-data
```

## Dominio

```text
domain-mining
domain-geology
domain-geometallurgy
domain-3d
domain-health
domain-infra
domain-ai
domain-design-system
```

## Cliente o producto

```text
client-spence
client-escondida
client-bhp
client-internal
client-outlier
product-imp
product-caring
product-kiri
product-drilling
```

## Reglas

- Cada repositorio activo debe tener al menos un estado, un tipo y un dominio.
- Los repositorios legacy deben indicar repositorio reemplazante si existe.
- Los repositorios experimentales deben tener responsable y fecha de revision.
- Los repositorios candidatos a archivar deben cerrar o migrar issues pendientes antes de archivarse.

## Ejemplo

```text
Repositorio: imp-spence-frontend
Descripcion: Frontend de plataforma IMP Spence.
Topics: status-active, type-frontend, domain-mining, client-spence, product-imp
```
