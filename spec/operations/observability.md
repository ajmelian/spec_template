# Observabilidad

## Logs

- Incluir correlation ID/request ID.
- Incluir usuario/cliente cuando sea seguro y necesario.
- No incluir secretos, tokens, passwords ni payloads sensibles completos.
- Separar logs de aplicacion, seguridad y auditoria si aplica.

## Metricas recomendadas

- Latencia por endpoint.
- Ratio de errores 4xx/5xx.
- Volumen de requests por cliente/IP.
- Login fallidos.
- Rate limit activados.
- Uso de integraciones externas.

## Alertas

| Alerta | Umbral | Severidad | Accion |
| --- | --- | --- | --- |
| 5xx alto | <umbral> | alta | revisar logs y rollback si aplica |
| Login fallidos | <umbral> | media/alta | investigar fuerza bruta |
| Latencia alta | <umbral> | media | revisar DB/integraciones |

## Auditoria

Eventos minimos:

- Login exitoso/fallido.
- Logout.
- Cambio de password.
- Cambio de permisos/roles.
- Operaciones criticas de negocio.
- Bloqueos o rate limits.
