# spec/ - Documentacion SDD del proyecto

Esta carpeta contiene la especificacion viva del proyecto.

## Carpetas

- `constitution/`: reglas estables, principios, stack, seguridad, calidad y roadmap.
- `architecture/`: arquitectura, modelo de datos, integraciones, despliegue y decisiones ADR.
- `api/`: contrato OpenAPI y convenciones de API.
- `features/`: una carpeta por feature.
- `testing/`: estrategia transversal de pruebas.
- `operations/`: runbooks, observabilidad, despliegue y rollback.
- `risk/`: registro de riesgos del proyecto.

## Orden recomendado de lectura

1. `constitution/mission.md`
2. `constitution/tech-stack.md`
3. `constitution/security.md`
4. `constitution/quality-gates.md`
5. `architecture/overview.md`
6. `api/openapi.yaml`
7. Feature activa en `features/`

## Regla de coherencia

Si una feature necesita romper una regla de `constitution/`, primero se debe crear una decision ADR justificando el cambio.
