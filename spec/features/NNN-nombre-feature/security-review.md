# NNN - <Nombre de la feature> - Revision de seguridad

## Resumen

<Resumen de los riesgos y controles de seguridad de la feature.>

## Superficie de ataque

- Endpoints expuestos: <lista>.
- Formularios: <lista>.
- Ficheros/subidas: <si/no>.
- Integraciones externas: <si/no>.
- Datos personales/sensibles: <si/no; cuales>.

## Modelo de amenazas simplificado

| Amenaza | Aplica | Control |
| --- | --- | --- |
| Spoofing | <si/no> | <auth fuerte, tokens, sesiones> |
| Tampering | <si/no> | <validacion, firmas, permisos> |
| Repudiation | <si/no> | <auditoria, correlation ID> |
| Information disclosure | <si/no> | <errores seguros, masking> |
| Denial of service | <si/no> | <rate limit, limites payload> |
| Elevation of privilege | <si/no> | <autorizacion backend> |

## Checklist

- [ ] Autenticacion requerida cuando aplica.
- [ ] Autorizacion comprobada en backend.
- [ ] Validacion de parametros de ruta/query/body/header.
- [ ] No hay SQL dinamico inseguro.
- [ ] No hay path traversal/SSRF si se procesan rutas o URLs.
- [ ] No se registran secretos ni tokens.
- [ ] Errores sin informacion interna.
- [ ] Rate limit considerado en endpoints sensibles.
- [ ] CORS/CSRF revisado segun tipo de cliente.
- [ ] OpenAPI no expone detalles inseguros.

## Hallazgos

| ID | Severidad | Descripcion | Estado | Resolucion |
| --- | --- | --- | --- | --- |
| SEC-FIND-001 | <baja/media/alta/critica> | <hallazgo> | <abierto/cerrado> | <accion> |
