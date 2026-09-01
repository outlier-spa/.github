# Checklist de repositorio

Usa esta lista para crear, revisar o normalizar repositorios en `outlier-spa`.

## Identidad

- [ ] El nombre usa kebab-case.
- [ ] El nombre evita mayusculas, espacios, puntos y guiones bajos.
- [ ] La descripcion explica para que sirve el repositorio.
- [ ] El repositorio tiene topics de estado, tipo, dominio y producto/cliente.
- [ ] El README explica instalacion, ejecucion, pruebas y despliegue.

## Gobierno

- [ ] Tiene responsable o equipo mantenedor.
- [ ] Tiene ciclo de vida definido: activo, mantenido, legacy, experimental, template o archivado.
- [ ] Usa labels estandar si maneja backlog.
- [ ] Usa issues para trabajo trazable.
- [ ] Usa pull requests para cambios relevantes.

## Seguridad

- [ ] No contiene secretos, tokens, claves, certificados ni credenciales.
- [ ] Tiene instrucciones de configuracion sin valores sensibles.
- [ ] Tiene `.gitignore` adecuado para la tecnologia.
- [ ] Las ramas principales estan protegidas si el repo es critico.
- [ ] Tiene CODEOWNERS si contiene infraestructura, seguridad, datos o librerias compartidas.

## Calidad tecnica

- [ ] Tiene comandos claros de build/test/run.
- [ ] Tiene pipeline o documenta por que no aplica.
- [ ] Tiene estrategia de versionado o releases si publica paquetes.
- [ ] Tiene dependencias actualizadas o plan de mantencion.
- [ ] Tiene documentado el proceso de despliegue si aplica.

## Archivo o cierre

- [ ] Si esta obsoleto, los issues fueron cerrados o migrados.
- [ ] Si fue reemplazado, el README indica el nuevo repositorio.
- [ ] Si es solo historico, debe marcarse como `status-legacy` o archivarse.
- [ ] Si es prueba o temporal, debe tener fecha de eliminacion o revision.
