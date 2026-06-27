# Runbook de despliegue

## Precondiciones

- Release aprobada.
- CI en verde.
- Backup validado si hay migraciones o cambio sensible.
- Ventana de mantenimiento definida si aplica.
- Rollback preparado.

## Pasos

1. Poner aplicacion en modo mantenimiento si aplica.
2. Descargar/activar version.
3. Instalar dependencias.
4. Aplicar migraciones.
5. Limpiar cache/config.
6. Reiniciar servicios si aplica.
7. Ejecutar smoke tests.
8. Revisar logs.
9. Desactivar mantenimiento.
10. Monitorizar durante el periodo definido.

## Smoke tests

- [ ] `GET /health` responde OK.
- [ ] Login funciona si aplica.
- [ ] Endpoint critico responde correctamente.
- [ ] No hay errores nuevos en logs.

## Evidencias

Registrar fecha, version, responsable, comandos ejecutados y resultado.
