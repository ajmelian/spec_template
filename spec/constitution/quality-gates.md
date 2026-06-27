# Quality gates y Definition of Done tecnico

Una tarea o feature no se considera terminada hasta superar estos controles.

## Definition of Ready

Antes de implementar:

- [ ] Existe `spec.md`.
- [ ] Existen criterios de aceptacion medibles.
- [ ] Existe `plan.md`.
- [ ] Existen tareas pequenas en `tasks.md`.
- [ ] Impacto en API, datos, seguridad y despliegue identificado.
- [ ] Dudas bloqueantes resueltas o marcadas.

## Definition of Done tecnico

- [ ] Todos los criterios de aceptacion estan cumplidos.
- [ ] Tests unitarios creados o justificacion de no aplicabilidad.
- [ ] Tests de integracion/API creados si hay endpoints o persistencia.
- [ ] Casos negativos y bordes cubiertos.
- [ ] OpenAPI actualizado si cambia la API.
- [ ] Migraciones creadas y probadas si cambia el modelo de datos.
- [ ] Revision de seguridad completada.
- [ ] No hay secretos en codigo, logs ni commits.
- [ ] Analisis estatico/lint sin errores criticos.
- [ ] Documentacion actualizada.
- [ ] `verification.md` contiene evidencias.
- [ ] `traceability.md` esta actualizado.
- [ ] Roadmap actualizado.

## Evidencias aceptadas

- Salida de comandos de test/lint.
- Capturas o logs de peticiones API.
- Fragmentos de respuesta HTTP.
- Referencias a commits/PRs.
- Resultado de revision manual.

## Severidad de hallazgos

| Severidad | Definicion | Criterio de cierre |
| --- | --- | --- |
| Critica | Explotable o bloquea produccion | Debe corregirse antes de merge |
| Alta | Riesgo serio o bug funcional relevante | Debe corregirse antes de release |
| Media | Impacto limitado o mitigable | Corregir o registrar excepcion |
| Baja | Mejora menor | Puede ir a backlog |
