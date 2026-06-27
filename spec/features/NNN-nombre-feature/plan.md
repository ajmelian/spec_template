# NNN - <Nombre de la feature> - Plan tecnico

**Spec:** `spec.md`
**Jira:** <ABC-123>
**Estado:** <borrador | aprobado | en ejecucion | cerrado>

## Enfoque

<Descripcion del enfoque tecnico. Debe explicar como se cumpliran los requisitos sin contradecir la constitucion.>

## Archivos/modulos afectados

| Ruta | Accion | Motivo |
| --- | --- | --- |
| `app/Controllers/...` | <crear/modificar> | <motivo> |
| `app/Services/...` | <crear/modificar> | <motivo> |
| `app/Models/...` | <crear/modificar> | <motivo> |
| `spec/api/openapi.yaml` | modificar | actualizar contrato |

## Diseno API

| Metodo | Ruta | Request | Response | Errores |
| --- | --- | --- | --- | --- |
| <POST> | `/api/v1/...` | <schema> | <schema> | <400/401/403/etc> |

## Validaciones

| Campo | Regla | Mensaje/error | AC relacionado |
| --- | --- | --- | --- |
| <campo> | <tipo/regex/rango> | <error> | AC-001 |

## Autorizacion

- Permiso requerido: <permiso/rol/politica>.
- Comprobacion en: <filter/service/policy>.
- Casos denegados: <casos>.

## Modelo de datos

- Migraciones: <si/no>.
- Indices: <si/no>.
- Compatibilidad hacia atras: <impacto>.
- Rollback de migracion: <estrategia>.

## Manejo de errores

| Caso | HTTP | Codigo interno | Mensaje seguro |
| --- | --- | --- | --- |
| <caso> | 400 | VALIDATION_ERROR | The request is invalid. |

## Seguridad

- Riesgos principales: <lista>.
- Controles aplicados: <lista>.
- Datos sensibles en logs: <si/no; mitigacion>.
- Rate limit: <si/no; regla>.
- CSRF/CORS: <aplica/no aplica; regla>.

## Pruebas previstas

- Unitarias: <servicios/reglas>.
- Integracion: <endpoints/repositorios>.
- Seguridad: <authz/input/rate limit>.
- Regresion: <areas sensibles>.

## Despliegue

- Variables `.env` nuevas: <lista>.
- Migraciones: <si/no>.
- Cache/config a limpiar: <si/no>.
- Feature flag: <si/no>.
- Rollback: <resumen>.

## Riesgos y mitigaciones

| Riesgo | Probabilidad | Impacto | Mitigacion |
| --- | --- | --- | --- |
| <riesgo> | <baja/media/alta> | <bajo/medio/alto> | <mitigacion> |

## Decisiones tomadas

- **DEC-001:** <decision y justificacion>.

## Dudas bloqueantes

- [ ] <Duda>.
