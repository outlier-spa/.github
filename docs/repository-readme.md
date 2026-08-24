# README minimo de repositorio

Todo repositorio activo o mantenido debe tener un README suficiente para que otra persona entienda que es, como se usa y quien lo mantiene.

## Estructura recomendada

```markdown
# Nombre del proyecto

Descripcion breve del objetivo del repositorio.

## Estado

status-active | status-maintained | status-legacy | status-experiment | status-template

## Responsable

Equipo o persona mantenedora.

## Tecnologia

- Lenguaje o framework principal
- Versiones relevantes
- Dependencias externas importantes

## Requisitos

- SDK o runtime
- Base de datos
- Servicios externos
- Variables de entorno necesarias, sin valores secretos

## Configuracion local

Pasos para ejecutar el proyecto localmente.

## Comandos

```bash
# instalar dependencias

# ejecutar

# probar

# build
```

## Despliegue o publicacion

Como se despliega, publica o libera el proyecto.

## Backlog y soporte

Indicar si el backlog vive en GitHub Issues, GitHub Projects u otra herramienta.

## Seguridad

No incluir secretos ni credenciales. Para problemas de seguridad, revisar SECURITY.md.
```

## Campos minimos

| Campo | Obligatorio | Comentario |
|---|---:|---|
| Descripcion | Si | Que hace el repositorio. |
| Estado | Si | Clasificacion de ciclo de vida. |
| Responsable | Si | Equipo o mantenedor. |
| Tecnologia | Si | Stack principal. |
| Configuracion local | Si | Necesario para continuidad. |
| Despliegue | Si aplica | Obligatorio en apps productivas. |
| Seguridad | Si | Nunca exponer secretos. |

## Repos legacy o archivados

Deben iniciar con una advertencia clara:

```markdown
> Estado: legacy / archivado
> Este repositorio no recibe nuevas funcionalidades.
> Repositorio reemplazante: <repo>, si aplica.
```

## Repos experimentales

Deben indicar:

- objetivo del experimento;
- responsable;
- fecha de revision;
- criterio de exito o descarte.
