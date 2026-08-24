# Outlier

Outlier desarrolla software, plataformas de datos, componentes reutilizables, automatizaciones e integraciones para proyectos industriales, mineros y de analitica operacional.

Este espacio de GitHub agrupa repositorios de productos, componentes, librerias, infraestructura, documentacion, herramientas internas y proyectos experimentales.

## Como esta organizada la cuenta

Los repositorios de Outlier deben poder clasificarse por tres dimensiones:

- **Producto o proyecto**: aplicacion, plataforma, modulo o iniciativa de negocio.
- **Tipo tecnico**: frontend, API, collector, libreria, componente, infraestructura, datos, documentacion o herramienta.
- **Estado de ciclo de vida**: activo, mantenido, legacy, experimental, plantilla, candidato a archivar o archivado.

## Estandares principales

Los lineamientos de trabajo se centralizan en este repositorio `.github`:

- [Guia de contribucion](../CONTRIBUTING.md)
- [Gobierno de GitHub](../GOVERNANCE.md)
- [Soporte](../SUPPORT.md)
- [Seguridad](../SECURITY.md)
- [Estandar de labels](../docs/labels.md)
- [Estandar de nombres de repositorios](../docs/repository-naming.md)
- [Ciclo de vida de repositorios](../docs/repository-lifecycle.md)
- [Flujo de backlog](../docs/backlog-workflow.md)
- [Ramas y pull requests](../docs/branching.md)
- [Equipos y permisos](../docs/teams-permissions.md)
- [Guia de CODEOWNERS](../docs/codeowners.md)

## Reglas base

- No subir secretos, tokens, claves, certificados ni archivos de configuracion sensibles.
- Usar issues para registrar trabajo trazable.
- Usar pull requests para cambios en ramas protegidas.
- Mantener README actualizado en repos activos.
- Clasificar repositorios mediante descripcion y topics.
- Archivar repositorios obsoletos para reducir ruido operacional.

## Flujo sugerido

```text
Idea / solicitud -> Issue -> Triage -> Ready -> In progress -> Pull request -> Review -> Done
```

## Nota

Este repositorio es publico porque GitHub requiere que el repositorio organizacional `.github` sea publico para aplicar archivos comunitarios por defecto a los repositorios de la organizacion que no tengan sus propias plantillas.
