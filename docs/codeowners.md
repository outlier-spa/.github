# Guia de CODEOWNERS

`CODEOWNERS` permite definir responsables automaticos de revision para rutas o archivos criticos dentro de un repositorio.

## Importante

El archivo `CODEOWNERS` de este repositorio `.github` no reemplaza automaticamente a los `CODEOWNERS` de todos los repositorios. Para repos criticos, cada repositorio debe tener su propio archivo si necesita reglas especificas de revision.

## Ubicaciones validas

En cada repositorio, GitHub reconoce `CODEOWNERS` en una de estas ubicaciones:

```text
.github/CODEOWNERS
CODEOWNERS
docs/CODEOWNERS
```

Se recomienda usar:

```text
.github/CODEOWNERS
```

## Ejemplo base

```text
# Responsable general del repositorio
* @organizacion/equipo-responsable

# Infraestructura y despliegue
.github/workflows/ @organizacion/equipo-infra
Dockerfile @organizacion/equipo-infra

# Base de datos
*.sql @organizacion/equipo-data
migrations/ @organizacion/equipo-data

# Seguridad y autenticacion
src/**/Auth*/ @organizacion/equipo-seguridad
src/**/Security*/ @organizacion/equipo-seguridad

# Documentacion
*.md @organizacion/equipo-documentacion
```

## Reglas recomendadas

- Usar equipos de GitHub, no usuarios individuales, cuando sea posible.
- Mantener pocos owners por ruta para no bloquear el flujo.
- Definir responsables por areas criticas: infraestructura, seguridad, datos, componentes, frontend y backend.
- Evitar reglas demasiado amplias si nadie revisara realmente esos cambios.
- Revisar CODEOWNERS al menos una vez por trimestre.

## Criterio para repos criticos

Se recomienda CODEOWNERS en repos que contengan:

- infraestructura;
- despliegues;
- autenticacion o autorizacion;
- integracion con datos productivos;
- librerias compartidas;
- componentes base de UI;
- automatizaciones de negocio;
- configuraciones de seguridad.

## Pendiente organizacional

Antes de activar CODEOWNERS de forma masiva, confirmar nombres reales de equipos en GitHub y responsables por producto o dominio.
