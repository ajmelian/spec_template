# Plan de rollback

## Objetivo

Restaurar el servicio a un estado funcional conocido si el despliegue falla.

## Tipos de rollback

- **Codigo:** volver a version anterior.
- **Configuracion:** restaurar variables o parametros anteriores.
- **Base de datos:** revertir migracion o restaurar backup.
- **Feature flag:** desactivar funcionalidad sin revertir codigo.

## Checklist

- [ ] Version anterior identificada.
- [ ] Backup disponible y probado si aplica.
- [ ] Migraciones reversibles o estrategia alternativa documentada.
- [ ] Responsable de decision definido.
- [ ] Criterios de activacion de rollback definidos.

## Criterios de activacion

- Error critico en flujo principal.
- Perdida o corrupcion de datos.
- Exposicion de seguridad.
- Degradacion severa de rendimiento.
- Error no mitigable en ventana aceptable.
