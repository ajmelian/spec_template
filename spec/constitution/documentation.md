# Politica de documentacion

## Documentos que deben mantenerse vivos

- `spec/constitution/*`: reglas estables.
- `spec/architecture/*`: arquitectura y decisiones.
- `spec/api/openapi.yaml`: contrato API.
- `spec/features/*`: feature specs, planes, tareas y verificaciones.
- `README.md`: uso general del proyecto.
- `.env.example`: variables sin secretos reales.

## Cuando actualizar documentacion

Actualizar documentacion cuando:

- Cambia un endpoint.
- Cambia el modelo de datos.
- Cambia una regla de negocio.
- Cambia una dependencia externa.
- Cambia seguridad/autorizacion.
- Cambia despliegue, cron, colas o configuracion.

## Idioma

- Documentacion interna: espanol, salvo convenciones tecnicas.
- Codigo: nombres en ingles o criterio definido por el proyecto, pero consistente.
- Comentarios: solo cuando aporten contexto no obvio.
