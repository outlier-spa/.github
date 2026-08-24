# Guia de contribucion

Esta guia define una forma minima y comun de trabajar en los repositorios de Outlier.

## Principios

- Todo cambio relevante debe estar trazado en un issue o pull request.
- Los cambios deben ser pequenos, revisables y con objetivo claro.
- No se deben subir secretos, tokens, llaves privadas, certificados ni archivos de configuracion sensibles.
- La documentacion debe actualizarse junto con el cambio cuando corresponda.
- Cada repositorio activo debe tener un README suficiente para instalar, ejecutar, probar y desplegar el proyecto.

## Flujo de trabajo recomendado

```text
Issue -> Triage -> Ready -> Branch -> Pull request -> Review -> Merge -> Done
```

## Issues

Usa una plantilla segun el tipo de trabajo:

- Bug report: errores o comportamientos inesperados.
- Feature request: nuevas funcionalidades o mejoras visibles.
- Task: tareas tecnicas, operativas o de documentacion.
- Technical debt: deuda tecnica, refactors o limpieza.

Un buen issue debe incluir:

- contexto;
- objetivo;
- alcance;
- criterios de aceptacion;
- prioridad;
- area afectada;
- evidencia, capturas o logs si aplica.

## Branches

Convencion sugerida:

```text
feature/descripcion-corta
fix/descripcion-corta
chore/descripcion-corta
docs/descripcion-corta
refactor/descripcion-corta
```

Ejemplos:

```text
feature/exportar-reporte-pdf
fix/error-calendario-l3
docs/actualizar-readme
refactor-normalizar-select
```

## Pull requests

Un pull request debe responder:

- que cambia;
- por que cambia;
- como se probo;
- que riesgos tiene;
- que issue cierra o relaciona.

Antes de solicitar revision, valida:

- build o pruebas relevantes ejecutadas;
- lint o formato si aplica;
- documentacion actualizada;
- sin secretos ni datos sensibles;
- cambios acotados al objetivo.

## Commits

Preferir mensajes claros:

```text
feat: agregar exportacion de reporte
fix: corregir calculo de fecha en calendario
chore: actualizar dependencias
docs: documentar configuracion local
refactor: simplificar servicio de usuarios
```

## Documentacion minima por repositorio

Cada repositorio activo deberia tener un README con:

- descripcion del proyecto;
- tecnologia principal;
- requisitos;
- configuracion local;
- comandos de build/test/run;
- variables de entorno esperadas sin valores secretos;
- proceso de despliegue o publicacion;
- responsables o equipo mantenedor;
- estado del repositorio.

## Seguridad

Si detectas una vulnerabilidad o filtracion de secretos, no abras un issue publico. Sigue las instrucciones de [SECURITY.md](SECURITY.md).
