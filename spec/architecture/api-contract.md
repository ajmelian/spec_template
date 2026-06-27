# Contrato API

El contrato canonico esta en `spec/api/openapi.yaml`.

## Principios

- OpenAPI se actualiza antes o durante la implementacion, nunca despues del cierre.
- Cada endpoint debe tener descripcion, parametros, request body, responses y errores.
- Las respuestas deben ser consistentes.
- Los cambios incompatibles requieren nueva version o plan de deprecacion.

## Versionado

Opciones aceptadas:

- Ruta: `/api/v1/...`
- Header: `Accept: application/vnd.<producto>.v1+json`

Elegir una y documentarla.

## Formato comun de respuesta de error

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "The request is invalid.",
    "details": [
      {
        "field": "email",
        "reason": "Invalid email format."
      }
    ],
    "correlationId": "req_123"
  }
}
```

## Paginacion

```text
GET /api/v1/resources?page=1&perPage=25
```

Respuesta recomendada:

```json
{
  "data": [],
  "meta": {
    "page": 1,
    "perPage": 25,
    "total": 100
  }
}
```

## Idempotencia

Para operaciones criticas o de pago:

```text
Idempotency-Key: <uuid>
```

## Cabeceras recomendadas

- `Authorization: Bearer <token>`
- `X-Client-Id: <client-id>` si aplica.
- `X-Correlation-Id: <id>` si el cliente lo proporciona.
- `Idempotency-Key: <uuid>` si aplica.
