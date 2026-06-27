# Arquitectura de despliegue

## Entornos

| Entorno | URL | Rama | Base de datos | Proposito |
| --- | --- | --- | --- | --- |
| local | <url> | feature/* | local | desarrollo |
| dev | <url> | develop | dev | integracion |
| staging | <url> | release/* | staging | validacion |
| prod | <url> | main/master | prod | produccion |

## Servidor web

- Document root debe apuntar a `public/`.
- `writable/` debe tener permisos minimos necesarios.
- Bloquear acceso directo a `.env`, `app/`, `tests/`, `vendor/` y ficheros internos.
- TLS obligatorio en entornos expuestos.

## Configuracion

- Variables por entorno.
- `.env.example` actualizado.
- Cache, sesiones y logs configurados segun entorno.
- Modo debug desactivado en produccion.

## Despliegue

Pasos generales:

1. Obtener release aprobada.
2. Backup si hay migraciones destructivas o riesgo relevante.
3. Instalar dependencias sin dev si aplica.
4. Ejecutar migraciones.
5. Limpiar/regenerar cache.
6. Reiniciar servicios si aplica.
7. Ejecutar smoke tests.
8. Monitorizar logs y metricas.
