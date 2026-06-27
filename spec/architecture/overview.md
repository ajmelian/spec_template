# Arquitectura general

## Objetivo arquitectonico

<Describir el enfoque general: monolito modular, API REST, aplicacion web, integraciones, etc.>

## Vista de contexto

```text
[Usuario/Cliente] -> [Frontend/Web/API Consumer] -> [Aplicacion PHP/CI4] -> [MySQL/MariaDB]
                                                   -> [Servicios externos]
```

## Modulos principales

| Modulo | Responsabilidad | Entrada | Salida |
| --- | --- | --- | --- |
| Auth | Autenticacion y sesion/token | Credenciales | Identidad autenticada |
| Users | Gestion de usuarios | Requests admin/API | Usuarios/roles |
| API | Endpoints publicos | HTTP JSON | JSON versionado |
| Audit | Registro de eventos | Eventos internos | Logs/auditoria |

## Principios de diseno

- Separacion entre capa HTTP y dominio.
- Servicios con responsabilidades cohesionadas.
- Contratos API estables y versionados.
- Persistencia encapsulada tras modelos/repositorios.
- Seguridad aplicada en filtros, servicios y politicas.

## Dependencias externas

| Servicio | Uso | Criticidad | Fallback |
| --- | --- | --- | --- |
| <Servicio> | <Uso> | <Alta/Media/Baja> | <Plan> |

## Reglas de compatibilidad

- No romper endpoints publicos sin version nueva o periodo de deprecacion.
- No eliminar columnas usadas por versiones activas sin migracion controlada.
- No cambiar semantica de campos sin actualizar OpenAPI y release notes.
