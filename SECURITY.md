# Politica de seguridad

## Reporte de vulnerabilidades

Si encuentras una vulnerabilidad, filtracion de credenciales, exposicion de datos, configuracion insegura o comportamiento que pueda afectar la seguridad de un proyecto de Outlier, no abras un issue publico.

Reporta el problema por canales internos a:

- el responsable tecnico del repositorio;
- el maintainer del producto;
- un owner de la organizacion GitHub;
- el canal interno definido para incidentes de seguridad, si existe.

## Informacion que debe incluir el reporte

Incluye, cuando sea posible:

- repositorio afectado;
- rama o version afectada;
- descripcion del problema;
- pasos para reproducir;
- impacto potencial;
- evidencia tecnica, logs o capturas sin exponer secretos adicionales;
- si hay credenciales, tokens o llaves comprometidas;
- recomendacion inicial de mitigacion si existe.

## Manejo de secretos

No se deben subir a GitHub:

- tokens;
- claves privadas;
- certificados;
- connection strings;
- passwords;
- dumps de bases de datos;
- archivos `.env` con valores reales;
- configuraciones productivas sensibles;
- datos personales o datos de clientes.

Si un secreto fue subido por error:

1. Revocar o rotar el secreto inmediatamente.
2. Notificar al responsable del repositorio.
3. Evaluar alcance e impacto.
4. Eliminar el secreto del historial si corresponde.
5. Registrar acciones de mitigacion.

## Dependencias

Los repositorios activos deben revisar periodicamente:

- paquetes obsoletos;
- dependencias con vulnerabilidades conocidas;
- pull requests de bots de dependencias;
- runtimes sin soporte;
- imagenes Docker desactualizadas.

## Repositorios archivados

Los repositorios archivados no deberian recibir nuevas funcionalidades ni PRs de dependencias. Si se requiere corregir una vulnerabilidad en un repositorio archivado, primero se debe validar si el codigo sigue siendo usado.
