# NNN - <Nombre de la feature> - Tareas

Checklist ejecutable derivada de `plan.md`. Cada tarea debe ser pequena, verificable y trazable.

## Preparacion

- [ ] **TASK-001:** Confirmar que `spec.md` esta aprobado. Cubre: REQ-001..REQ-N.
- [ ] **TASK-002:** Confirmar que `plan.md` no contradice la constitucion.
- [ ] **TASK-003:** Crear rama `feature/<JIRA-ID>-<nombre-corto>`.

## Contrato y datos

- [ ] **TASK-010:** Actualizar `spec/api/openapi.yaml`. Cubre: AC-003.
- [ ] **TASK-011:** Crear/actualizar migracion si aplica. Cubre: <REQ/AC>.
- [ ] **TASK-012:** Actualizar modelo de datos en `spec/architecture/data-model.md` si aplica.

## Implementacion

- [ ] **TASK-020:** Crear/actualizar DTO/request validation. Cubre: AC-001, AC-002.
- [ ] **TASK-021:** Crear/actualizar servicio de dominio. Cubre: REQ-001.
- [ ] **TASK-022:** Crear/actualizar modelo/repositorio. Cubre: REQ-002.
- [ ] **TASK-023:** Crear/actualizar controlador/endpoint. Cubre: AC-001.
- [ ] **TASK-024:** Aplicar autorizacion/filtros. Cubre: SEC-001.
- [ ] **TASK-025:** Aplicar logging/auditoria segura si aplica. Cubre: SEC-002.

## Pruebas

- [ ] **TASK-030:** Crear tests unitarios. Cubre: TEST-001..TEST-N.
- [ ] **TASK-031:** Crear tests de integracion/API. Cubre: TEST-010..TEST-N.
- [ ] **TASK-032:** Crear pruebas negativas de validacion/autorizacion.
- [ ] **TASK-033:** Ejecutar suite y registrar evidencias en `verification.md`.

## Seguridad y calidad

- [ ] **TASK-040:** Completar `security-review.md`.
- [ ] **TASK-041:** Ejecutar analisis estatico/lint si existe.
- [ ] **TASK-042:** Revisar que no hay secretos ni datos sensibles en logs.
- [ ] **TASK-043:** Actualizar `traceability.md`.

## Cierre

- [ ] **TASK-050:** Actualizar `release-notes.md`.
- [ ] **TASK-051:** Actualizar `spec/constitution/roadmap.md`.
- [ ] **TASK-052:** Preparar PR con checklist completo.
