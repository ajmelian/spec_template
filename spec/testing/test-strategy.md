# Estrategia de pruebas

## Objetivo

Garantizar que cada cambio se valida contra requisitos funcionales, contrato API, seguridad y regresion.

## Niveles

- **Unitario:** servicios, validadores, reglas de dominio.
- **Integracion:** modelos, repositorios, endpoints, base de datos.
- **Contrato:** coherencia entre implementacion y OpenAPI.
- **Seguridad:** autenticacion, autorizacion, validacion, rate limit, errores.
- **Regresion:** flujos criticos existentes.
- **Smoke:** comprobaciones basicas tras despliegue.

## Minimos por feature API

- Test de peticion valida.
- Test de validacion fallida.
- Test no autenticado si requiere auth.
- Test autenticado sin permisos si aplica.
- Test de recurso inexistente si aplica.
- Test de aislamiento por tenant/propietario si aplica.

## Datos de prueba

- Seeds controlados.
- No usar datos reales de produccion.
- Datos sensibles ficticios.

## Criterios de aceptacion de calidad

- Tests criticos en verde.
- Sin errores de analisis estatico criticos.
- Sin endpoints sin documentar.
- Sin hallazgos de seguridad criticos/altos abiertos.
