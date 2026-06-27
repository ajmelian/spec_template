# Git workflow

## Modelo

Usar GitFlow o el flujo definido por el equipo.

Ramas recomendadas:

- `main` o `master`: produccion, protegida.
- `develop`: integracion.
- `feature/JIRA-123-nombre-corto`: nuevas features.
- `bugfix/JIRA-123-nombre-corto`: correcciones no urgentes.
- `hotfix/JIRA-123-nombre-corto`: correcciones urgentes en produccion.
- `release/x.y.z`: preparacion de version.

## Relacion con Jira

Toda rama y commit relevante debe incluir el ID de tarea:

```text
feature/ABC-123-login-api
ABC-123: add login endpoint validation
```

## Commits

Formato recomendado:

```text
ABC-123: verbo en imperativo y descripcion breve
```

Ejemplos:

```text
ABC-123: add API login request validation
ABC-123: update OpenAPI contract for auth endpoints
ABC-123: fix authorization check for tenant users
```

## Pull Request

Todo PR debe incluir:

- Feature/spec relacionada.
- Resumen tecnico.
- Cambios funcionales.
- Cambios de API.
- Migraciones.
- Riesgos.
- Evidencias de test.
- Checklist de seguridad.

## Protecciones

- No push directo a `main/master`.
- No merge sin CI verde.
- No merge sin revision humana para cambios sensibles.
- Squash o merge commit segun politica del proyecto.
