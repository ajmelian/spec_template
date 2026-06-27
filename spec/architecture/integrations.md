# Integraciones externas

## Registro de integraciones

| Servicio | Tipo | Propietario | Datos enviados | Datos recibidos | Criticidad |
| --- | --- | --- | --- | --- | --- |
| <Servicio> | <API/SMTP/SFTP/etc> | <Equipo> | <Datos> | <Datos> | <Alta/Media/Baja> |

## Reglas

- No llamar servicios externos directamente desde controladores.
- Encapsular cada integracion en un cliente/servicio.
- Definir timeouts.
- Gestionar reintentos con backoff si aplica.
- No registrar payloads sensibles completos.
- Documentar credenciales necesarias en `.env.example` sin valores reales.

## Variables de entorno

```text
SERVICE_BASE_URL=
SERVICE_API_KEY=
SERVICE_TIMEOUT_SECONDS=
```

## Fallback y degradacion

<Describir que ocurre si cada integracion falla.>
