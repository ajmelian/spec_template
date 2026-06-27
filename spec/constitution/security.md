# Seguridad

Controles minimos para aplicaciones online y APIs expuestas a terceros.

## Principios

- Seguridad por defecto.
- Minimo privilegio.
- Validacion explicita de entradas.
- Respuestas de error seguras.
- Trazabilidad sin exponer datos sensibles.
- Defensa en profundidad.

## Autenticacion

- Definir mecanismo: session, JWT, API key, OAuth2, mTLS u otro.
- Passwords siempre con hashing robusto mediante API nativa/framework.
- Tokens con expiracion, revocacion y rotacion cuando aplique.
- Login con rate limit y proteccion anti-fuerza bruta.
- No exponer si un email/usuario existe en flujos publicos.

## Autorizacion

- Comprobar permisos en backend, no solo en UI.
- Aplicar control por rol, permiso, tenant o propietario del recurso segun dominio.
- Separar autenticacion de autorizacion.
- Denegar por defecto.

## APIs multi-cliente

- Cada cliente debe tener identificador unico.
- Las credenciales de cliente no deben almacenarse en claro.
- Rate limiting por cliente, IP y endpoint sensible.
- Registrar uso por cliente para auditoria.
- Aislar datos por tenant/cliente si aplica.

## Validacion de input

- Validar todo parametro de ruta, query, header y body.
- Definir longitud maxima para strings.
- Rechazar campos no esperados si el contrato lo exige.
- Sanitizar solo como complemento; no sustituye a la validacion.
- Usar allow-list frente a deny-list cuando sea posible.

## Protecciones web

- CSRF obligatorio en formularios web con estado.
- Cookies `HttpOnly`, `Secure` y `SameSite` cuando aplique.
- Cabeceras de seguridad: CSP, HSTS, X-Frame-Options o equivalente moderno, Referrer-Policy y Permissions-Policy segun contexto.
- CORS restrictivo y documentado.

## Protecciones API

- OpenAPI actualizado.
- Esquema de errores comun.
- Limites de payload.
- Idempotency-Key en operaciones criticas si aplica.
- No permitir metodos HTTP no definidos.
- Versionado de API.

## Datos sensibles

- Clasificar campos: publico, interno, confidencial, secreto, dato personal.
- Cifrado en transito siempre con TLS.
- Cifrado en reposo cuando el riesgo lo requiera.
- Minimizar almacenamiento.
- Definir retencion y borrado.
- En logs, enmascarar datos sensibles.

## Secretos

- Usar `.env` local y variables de entorno en servidores.
- No commitear `.env`, claves privadas, certificados, tokens ni dumps.
- Rotar secretos si se sospecha exposicion.
- Mantener `.env.example` sin valores reales.

## Logging y auditoria

- Registrar eventos de seguridad: login fallido, bloqueo, cambio de permisos, operaciones criticas.
- No registrar passwords, tokens, API keys ni documentos sensibles completos.
- Usar correlation ID/request ID.
- Proteger logs contra acceso no autorizado.

## Checklist OWASP practico

- [ ] Injection mitigada con consultas parametrizadas/ORM seguro.
- [ ] Autenticacion robusta y rate limit en endpoints sensibles.
- [ ] Control de acceso probado en backend.
- [ ] Configuracion segura por entorno.
- [ ] Validacion de input completa.
- [ ] Respuestas de error sin fuga de informacion.
- [ ] Dependencias revisadas.
- [ ] Logs sin secretos.
- [ ] Proteccion contra SSRF/path traversal si hay URLs o ficheros.
- [ ] Subida de ficheros validada por extension, MIME, tamano y almacenamiento seguro.
