# Tech stack y convenciones tecnicas

Referencia tecnica estable del proyecto. Todo plan de feature debe respetar este documento.

## Stack base recomendado

- **Lenguaje:** PHP 8.x.
- **Framework:** CodeIgniter 4.x.
- **Autenticacion/autorizacion:** CodeIgniter Shield o modulo definido por el proyecto.
- **Base de datos:** MySQL/MariaDB.
- **Servidor HTTP:** Apache o Nginx segun entorno.
- **Dependencias:** Composer.
- **API contract:** OpenAPI 3.x.
- **Tests:** PHPUnit / CodeIgniter Test Framework.
- **Analisis estatico:** PHPStan o Psalm, si el proyecto lo permite.
- **Estilo:** PSR-12 como base, adaptado a las reglas del proyecto.
- **Contenedores:** <Permitidos / No permitidos>. Por defecto, no asumir Docker.

## Entornos

- **local:** desarrollo individual.
- **dev:** integracion temprana.
- **staging/pre:** validacion funcional y tecnica.
- **prod:** entorno productivo.

## Comandos del proyecto

Actualizar estos comandos con los reales del repositorio.

```bash
composer install
composer test
composer lint
php spark migrate
php spark serve
```

## Estructura recomendada CodeIgniter 4

```text
app/
├── Config/
├── Controllers/
├── Database/
│   ├── Migrations/
│   └── Seeds/
├── Entities/
├── Filters/
├── Libraries/
├── Models/
├── Services/
├── Validation/
└── Views/
public/
tests/
writable/
```

## Convenciones de nombres

- Variables: `camelCase`.
- Funciones y metodos: `camelCase`.
- Clases: `PascalCase`.
- Constantes: `UPPER_SNAKE_CASE`.
- Tablas: `snake_case` plural o criterio definido por el proyecto.
- Columnas: `snake_case`.
- Rutas API: kebab-case o snake_case, pero no mezclar.

## Patron de capas

- **Controller:** recibe request, invoca validacion y delega.
- **Validation/Request DTO:** valida y normaliza entradas.
- **Service:** contiene reglas de negocio.
- **Model/Repository:** acceso a datos.
- **Entity/DTO:** transporte estructurado de datos.
- **Presenter/Resource:** transforma respuestas API.

## Limites duros

- No escribir SQL concatenando input externo.
- No colocar logica de negocio compleja en controladores.
- No exponer errores internos al cliente API.
- No introducir dependencias sin ADR o aprobacion tecnica.
- No modificar migraciones ya aplicadas en produccion; crear nuevas migraciones.
- No usar codigo duplicado cuando pueda extraerse sin perder claridad.
