# Modelo de datos

## Convenciones

- Tablas y columnas en `snake_case`.
- Claves primarias segun criterio del proyecto: `id` incremental, UUID u otro.
- Timestamps consistentes: `created_at`, `updated_at`, `deleted_at` si aplica.
- Soft delete solo cuando exista necesidad funcional/auditoria.
- Indices documentados para busquedas frecuentes.

## Entidades

### <Entidad>

| Campo | Tipo | Requerido | Sensibilidad | Reglas |
| --- | --- | --- | --- | --- |
| id | bigint/uuid | Si | Interno | Clave primaria |
| created_at | datetime | Si | Interno | Fecha de creacion |

## Relaciones

```text
<Entidad A> 1 -- N <Entidad B>
```

## Migraciones

- Cada cambio de esquema va en una migracion nueva.
- No editar migraciones ya aplicadas en produccion.
- Incluir estrategia de rollback o explicar por que no es reversible.
- Validar migraciones en entorno no productivo antes de produccion.

## Clasificacion de datos

| Clasificacion | Ejemplos | Tratamiento |
| --- | --- | --- |
| Publico | Datos visibles publicamente | Sin restricciones especiales |
| Interno | IDs tecnicos, estados | No exponer si no aplica |
| Personal | Email, nombre, IP | Minimizar, proteger y auditar |
| Confidencial | Datos de negocio sensibles | Acceso restringido |
| Secreto | Passwords, tokens, API keys | Nunca en claro ni en logs |
