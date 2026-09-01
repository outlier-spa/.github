# Topics de repositorios

Los topics ayudan a filtrar, agrupar y auditar repositorios en la organizacion.

## Regla general

Cada repositorio activo debe tener al menos:

```text
status-<estado>
type-<tipo>
```

Y cuando aplique:

```text
client-<cliente>
product-<producto>
domain-<dominio>
```

## Estados

```text
status-active
status-maintained
status-legacy
status-experiment
status-template
status-archive-candidate
status-delete-candidate
```

## Tipos tecnicos

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
type-ai
```

## Dominios

```text
domain-mining
domain-geology
domain-geometallurgy
domain-3d
domain-health
domain-infra
domain-ai
domain-design-system
domain-automation
```

## Clientes o contexto

```text
client-spence
client-escondida
client-bhp
client-internal
client-outlier
```

## Productos

```text
product-imp
product-caring
product-kiri
product-drilling
product-visualizer
product-component
product-outdocs
product-chronos
```

## Ejemplos

### API de IMP Spence

```text
status-active
type-api
client-spence
client-bhp
product-imp
domain-mining
```

### Libreria geometrica

```text
status-maintained
type-library
domain-mining
```

### Componente UI

```text
status-active
type-component
product-component
domain-design-system
```

### Repositorio legacy

```text
status-legacy
type-app
client-spence
```

## Reglas

- Usar lowercase.
- Usar kebab-case.
- Evitar abreviaturas ambiguas.
- No usar nombres de personas como topics.
- No duplicar significados.
- Revisar topics cuando cambie el estado del repo.
