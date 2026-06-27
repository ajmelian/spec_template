# NNN - <Nombre de la feature> - Plan de pruebas

## Objetivo

Validar que la feature cumple los criterios de aceptacion, no rompe comportamiento existente y respeta seguridad minima.

## Matriz de pruebas

| ID | Tipo | Descripcion | Cubre | Resultado esperado |
| --- | --- | --- | --- | --- |
| TEST-001 | Unitario | <Regla de negocio valida> | AC-001 | <resultado> |
| TEST-002 | Unitario | <Regla de negocio invalida> | AC-002 | <error> |
| TEST-010 | Integracion/API | <Peticion valida> | AC-001 | HTTP 200/201 |
| TEST-011 | Integracion/API | <Peticion invalida> | AC-002 | HTTP 400 |
| TEST-020 | Seguridad | Usuario sin permiso | SEC-001 | HTTP 403 |

## Datos de prueba

- Usuario valido: <descripcion>.
- Usuario sin permisos: <descripcion>.
- Payload valido: <descripcion>.
- Payload invalido: <descripcion>.

## Casos negativos obligatorios

- [ ] Input requerido ausente.
- [ ] Input con tipo incorrecto.
- [ ] Input fuera de rango/longitud.
- [ ] Usuario no autenticado.
- [ ] Usuario autenticado sin permiso.
- [ ] Recurso inexistente.
- [ ] Intento de acceso a recurso de otro tenant/propietario si aplica.

## Comandos

```bash
composer test
# o comando real del proyecto
```
