# NNN - <Nombre de la feature> - Spec

**Estado:** <propuesta | en curso | implementada | descartada>
**Jira:** <ABC-123>
**Responsable:** <nombre/equipo>
**Fecha:** <YYYY-MM-DD>
**Version objetivo:** <x.y.z>

## Resumen

<Descripcion clara de la feature desde el punto de vista del usuario o cliente API. No incluir detalles de implementacion.>

## Problema

<Que problema concreto resuelve y por que debe resolverse ahora.>

## Objetivos

- **REQ-001:** <Requisito funcional o tecnico>.
- **REQ-002:** <Requisito funcional o tecnico>.
- **REQ-003:** <Requisito funcional o tecnico>.

## No objetivos / fuera de alcance

- <Cosa relacionada que no se hara en esta feature>.
- <Cosa que se delega a otra feature>.

## Usuarios / actores

| Actor | Necesidad | Permisos esperados |
| --- | --- | --- |
| <Actor> | <Necesidad> | <Permisos> |

## Historias de usuario

- **US-001:** Como <actor>, quiero <accion>, para <beneficio>.
- **US-002:** Como <actor>, quiero <accion>, para <beneficio>.

## Reglas de negocio

- **BR-001:** <Regla verificable>.
- **BR-002:** <Regla verificable>.

## Criterios de aceptacion

- [ ] **AC-001:** Dado <contexto>, cuando <accion>, entonces <resultado observable>.
- [ ] **AC-002:** Dado <contexto>, cuando <accion invalida>, entonces <error esperado>.
- [ ] **AC-003:** El comportamiento queda documentado en OpenAPI si afecta a la API.
- [ ] **AC-004:** La feature cumple `spec/constitution/security.md`.

## Impacto API

| Metodo | Ruta | Cambio | Autenticacion | Autorizacion |
| --- | --- | --- | --- | --- |
| <GET/POST/etc> | `/api/v1/...` | <nuevo/modifica/depreca> | <Si/No> | <Rol/permiso> |

## Impacto datos

- Nuevas tablas: <si/no>.
- Nuevas columnas: <si/no>.
- Migracion requerida: <si/no>.
- Datos personales tratados: <si/no y cuales>.

## Requisitos de seguridad

- **SEC-001:** <Control de seguridad especifico>.
- **SEC-002:** <Control de seguridad especifico>.

## Requisitos no funcionales

- Rendimiento: <latencia, volumen, limites>.
- Disponibilidad: <requisito si aplica>.
- Observabilidad: <logs, metricas, eventos>.
- Accesibilidad: <si hay UI>.

## Suposiciones

- <Suposicion que debe validarse>.

## Preguntas abiertas

- [ ] <Pregunta pendiente>.
