# Repository Review Standards

> **Propósito:** asegurar que cada revisión de repositorio realizada por IA sea consistente, verificable y accionable. La revisión debe basarse en evidencia real del código y configuración; no debe modificar archivos salvo que se solicite explícitamente.

## 1. Objetivo y alcance

Este estándar aplica a los repositorios de Outlier, especialmente librerías .NET, APIs, servicios, collectors y proyectos publicados como paquetes NuGet.

La revisión debe evaluar:

- Estructura, arquitectura, calidad de código, pruebas, automatización y documentación.
- Empaquetado y distribución cuando corresponda.
- Riesgos y oportunidades de mejora de manera proporcional al tamaño y propósito del repositorio.
- Hallazgos priorizados que puedan transformarse en backlog o issues.

Este estándar no reemplaza una revisión de seguridad especializada ni la validación funcional del negocio.

## 2. Principios de revisión

| Principio | Aplicación obligatoria |
| --- | --- |
| Basado en evidencia | Cada hallazgo debe indicar el archivo, configuración, flujo o ausencia verificable que lo sustenta. |
| Proporcional | Una librería pequeña no requiere la misma arquitectura que una plataforma o servicio operacional. |
| Sin cambios implícitos | Separar claramente el diagnóstico de cualquier propuesta de implementación. |
| Accionable | Cada recomendación debe incluir prioridad, beneficio esperado y esfuerzo relativo. |
| Compatible con Outlier | Considerar .NET 8, estructura `/src`, namespaces `Outlier.*` y publicación NuGet cuando aplique. |

## 3. Escala de evaluación

Cada dimensión se califica de **1 a 5**. El puntaje global es el promedio ponderado; ante un riesgo crítico, prevalece el criterio profesional.

| Puntaje | Interpretación | Decisión sugerida |
| --- | --- | --- |
| 5 | Sólido y mantenible | Mantener; aplicar mejoras menores solo cuando aporten valor. |
| 4 | Bueno, con brechas acotadas | Planificar mejoras de bajo riesgo. |
| 3 | Funcional, pero inconsistente | Crear backlog de mejoras priorizadas. |
| 2 | Riesgo relevante de mantenimiento | Definir un plan de corrección antes de ampliar el alcance. |
| 1 | Riesgo crítico o falta de controles | Corregir antes de nuevas funcionalidades o publicación. |

## 4. Matriz de revisión

| Dimensión | Peso | Qué se debe revisar |
| --- | ---: | --- |
| Propósito y límites | 10% | Nombre, responsabilidad, dependencias y coherencia del repositorio. |
| Estructura y arquitectura | 15% | Solución, `/src`, proyectos, carpetas, acoplamiento y visibilidad pública. |
| Calidad de código | 15% | Nombres, nulabilidad, errores, inmutabilidad, cultura/zonas horarias y duplicación. |
| Pruebas | 15% | Cobertura funcional, casos de borde, regresión, datos de prueba y ejecución automatizada. |
| Build y CI/CD | 15% | Build reproducible, pruebas en CI, versiones, tags, workflows y dependencias actualizadas. |
| Paquete y distribución | 10% | NuGet, metadatos, SourceLink, determinismo, símbolos, compatibilidad y changelog. |
| Documentación | 10% | README orientado al consumidor, instalación, ejemplos, decisiones y contribución. |
| Seguridad y gobierno | 10% | Secretos, permisos, dependencias, licencia, reglas de rama e incidencias conocidas. |

## 5. Controles mínimos por tipo de repositorio

| Tipo | Controles adicionales esperados |
| --- | --- |
| Librería NuGet | API estable, compatibilidad, documentación XML cuando se justifique, pruebas de borde y publicación solo desde tags o releases. |
| API o servicio | Configuración por ambiente, manejo de errores, telemetría, health checks, autenticación y pruebas de integración. |
| Collector / Agent | Tolerancia a caídas, reintentos, trazabilidad, configuración externa y operación sin intervención continua. |
| Aplicación web | Separación UI/dominio/datos, accesibilidad básica, seguridad de sesión y validación de flujos críticos. |

## 6. Procedimiento de revisión asistida por IA

1. Confirmar repositorio, rama revisada, tipo de proyecto y objetivo de la evaluación.
2. Revisar el árbol de archivos, solución/proyectos, README, configuración de build, workflows y dependencias.
3. Leer una muestra representativa del código productivo y de pruebas; profundizar en las áreas de mayor riesgo.
4. Ejecutar, cuando sea seguro y esté disponible, restore, build y test. Informar explícitamente si no fue posible.
5. Calificar las ocho dimensiones, fundamentar cada puntaje y registrar los hallazgos con evidencia.
6. Clasificar los hallazgos por prioridad y proponer un plan incremental.
7. No modificar el repositorio durante una revisión, salvo instrucción explícita.

## 7. Clasificación de hallazgos

| Nivel | Criterio | Ejemplos |
| --- | --- | --- |
| P0 - Crítico | Afecta seguridad, publicación, datos o continuidad operacional. | Secretos expuestos, paquete no reproducible, CI inexistente en una librería publicada. |
| P1 - Alto | Deuda probable que impactará cambios próximos. | Falta de pruebas en lógica crítica, errores de cultura/UTC, workflow obsoleto. |
| P2 - Medio | Mejora importante sin riesgo inmediato. | README incompleto, nombres inconsistentes, pruebas parciales. |
| P3 - Bajo | Pulido o consistencia; no debe bloquear desarrollo. | Orden de carpetas, comentarios redundantes o estilo menor. |

## 8. Formato obligatorio del informe

La IA debe generar un informe con esta estructura:

1. **Resumen ejecutivo:** propósito del repositorio, resultado global, puntaje y recomendación principal.
2. **Alcance y evidencia revisada:** rama o commit, archivos clave, comandos ejecutados y limitaciones.
3. **Matriz de puntajes:** las ocho dimensiones, puntaje, evidencia y comentario breve.
4. **Fortalezas:** prácticas que deben mantenerse.
5. **Hallazgos priorizados:** nivel P0-P3, evidencia, impacto, recomendación y esfuerzo estimado (S/M/L).
6. **Plan sugerido:** acciones de corto plazo, siguiente iteración y mejoras futuras.
7. **Decisiones arquitectónicas:** separar componentes únicamente cuando el beneficio compense la complejidad adicional.

El informe no debe limitarse a una lista genérica de buenas prácticas.

## 9. Prompt reutilizable

```text
Revisa el repositorio [ORGANIZACION/REPOSITORIO] en la rama [RAMA] siguiendo
el “Repository Review Standards” de Outlier. No modifiques archivos.

Identifica el tipo de repositorio y evalúa las ocho dimensiones de la matriz.
Basa cada observación en evidencia concreta del código, proyectos, pruebas,
README y workflows. Ejecuta build y test solo si están disponibles y es seguro hacerlo.

Genera un informe en español con: resumen ejecutivo, alcance revisado, matriz
de puntajes, fortalezas, hallazgos P0-P3 con evidencia e impacto, y un plan
de mejora priorizado. Evita sugerencias genéricas o reestructuraciones masivas
sin justificación.
```

## 10. Criterio de cierre

La revisión se considera completa cuando el informe contiene evidencia suficiente, puntajes trazables, prioridades claras y una recomendación proporcional al tamaño y propósito del repositorio.

Las propuestas de cambio deben transformarse en issues o backlog solo después de validar su prioridad con el responsable técnico.
