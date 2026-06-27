# Plantilla SDD profesional para APIs y aplicaciones online PHP

Esta plantilla proporciona una estructura de documentación técnica para trabajar con **Spec-Driven Development (SDD)** en proyectos de aplicaciones online y APIs, especialmente en entornos PHP, CodeIgniter 4, MySQL/MariaDB y desarrollo asistido por IA.

El objetivo de la plantilla no es generar código directamente, sino crear una **fuente de verdad técnica** que gobierne el desarrollo: primero se documenta la intención, después se define el plan, luego se desglosan las tareas y finalmente se implementa y verifica.

La carpeta principal que se debe incorporar al proyecto es:

```text
spec/
```

El directorio `spec/` contiene todos los artefactos SDD. El resto del proyecto debe contener el código real de la aplicación, sus dependencias, configuración, tests y documentación operativa propia.

## Autoría

**Autor principal:** Aythami Melian Perdomo  
**Perfil profesional:** Ingeniero de Software PHP especializado en aplicaciones online, APIs, desarrollo seguro, DevSecOps y Spec-Driven Development.  
**Asistencia técnica:** plantilla elaborada con apoyo de IA generativa bajo dirección, revisión y criterio técnico del autor.  
**Versión de la plantilla:** 1.0.2  
**Fecha:** 2026-06-27

Salvo que el proyecto defina otra licencia específica, esta plantilla se entrega como base reutilizable, modificable y adaptable a proyectos propios o profesionales, manteniendo la atribución de autoría cuando se distribuya como plantilla independiente.

## Principio de diseño

Esta plantilla está pensada para trabajar en modo **spec-anchored**:

1. La especificación se crea antes del código.
2. La especificación se mantiene viva durante el desarrollo.
3. Cualquier cambio funcional, técnico o de seguridad relevante debe reflejarse primero en `spec/`.
4. El código se considera un artefacto derivado de la especificación.
5. La validación se realiza contra criterios de aceptación, pruebas, gates de calidad y revisión de seguridad.

Este enfoque reduce ambigüedad, pérdida de contexto, cambios invisibles de rumbo, deuda cognitiva y comportamiento indeterminado de los agentes de IA.

## Qué incluye la plantilla

La plantilla contiene únicamente documentación SDD. No incluye `AGENTS.md`, `.opencode/`, comandos personalizados, configuración de IDE ni arneses de agente.

Esto es deliberado.

Al ejecutar `/init` en OpenCode, el agente debe leer el proyecto real, analizar el código existente, detectar el stack efectivo y generar su propio `AGENTS.md`. Si la plantilla incluyera un `AGENTS.md` genérico, podría contaminar el arnés del proyecto con reglas no ajustadas al código real.

## Estructura

```text
spec/
├── README.md
├── constitution/
│   ├── mission.md
│   ├── tech-stack.md
│   ├── coding-standards.md
│   ├── security.md
│   ├── quality-gates.md
│   ├── git-workflow.md
│   ├── documentation.md
│   ├── roadmap.md
│   └── glossary.md
├── architecture/
│   ├── overview.md
│   ├── data-model.md
│   ├── api-contract.md
│   ├── integrations.md
│   ├── deployment.md
│   └── decisions/
│       └── ADR-000-template.md
├── api/
│   └── openapi.yaml
├── features/
│   └── NNN-nombre-feature/
│       ├── spec.md
│       ├── plan.md
│       ├── tasks.md
│       ├── test-plan.md
│       ├── security-review.md
│       ├── verification.md
│       ├── traceability.md
│       └── release-notes.md
├── testing/
│   └── test-strategy.md
├── operations/
│   ├── deployment-runbook.md
│   ├── rollback-plan.md
│   └── observability.md
└── risk/
    └── risk-register.md
```

## Finalidad de cada bloque

Los siguientes ejemplos usan como referencia una aplicación online realista denominada **Portal de Incidencias**, desarrollada con **PHP**, **CodeIgniter 4**, **MySQL**, **PHPUnit**, **HTML5**, **Bootstrap 5**, repositorio en **GitHub** y despliegue al servidor de desarrollo mediante **SFTP**.

La aplicación de ejemplo permite que usuarios autenticados registren incidencias, adjunten información básica, consulten el estado de sus tickets y que perfiles internos gestionen la resolución.

### `spec/constitution/`

Define las reglas estables del proyecto. Debe completarse al inicio y modificarse poco.

Contiene la misión del producto, stack técnico, estándares de código, criterios de seguridad, gates de calidad, flujo Git, reglas de documentación, roadmap y glosario.

La constitución manda sobre las features. Si una feature necesita romper una regla de `constitution/`, primero debe justificarse con una decisión de arquitectura en `architecture/decisions/`.

**Ejemplo aplicado:**

En el proyecto **Portal de Incidencias**, `constitution/` definiría que la aplicación se desarrolla en PHP con CodeIgniter 4, que la base de datos es MySQL, que el repositorio oficial está en GitHub, que las pruebas unitarias se ejecutan con PHPUnit, que la subida al servidor de desarrollo se realiza por SFTP y que el frontend se implementa con HTML5 y Bootstrap 5.

Ejemplo de contenido esperado:

```text
mission.md
- Producto: Portal de Incidencias.
- Usuarios: empleados, técnicos de soporte y administradores.
- Objetivo: registrar, consultar y resolver incidencias internas.
- Exclusiones: no incluye chat en tiempo real ni sistema avanzado de SLA en la primera versión.

tech-stack.md
- Backend: PHP 8.x + CodeIgniter 4.
- Base de datos: MySQL.
- Repositorio: GitHub.
- Despliegue desarrollo: SFTP a dev.incidencias.example.com.
- Testing: PHPUnit.
- Frontend: HTML5 + Bootstrap 5.

quality-gates.md
- vendor/bin/phpunit debe finalizar correctamente.
- No se acepta una feature sin validación backend.
- No se acepta un endpoint nuevo sin actualizar OpenAPI.
- No se suben ficheros .env al repositorio.
```

### `spec/architecture/`

Documenta cómo está construido el sistema.

Incluye visión de arquitectura, modelo de datos, contrato API, integraciones, despliegue y decisiones ADR. Debe servir para que un ingeniero o un agente de IA entienda el sistema antes de modificarlo.

**Ejemplo aplicado:**

En el **Portal de Incidencias**, `architecture/` describiría una arquitectura MVC propia de CodeIgniter 4, separando controladores, modelos, entidades, servicios, validadores, vistas HTML5/Bootstrap 5 y endpoints API.

Ejemplo de contenido esperado:

```text
overview.md
- app/Controllers/Web/: controladores para pantallas HTML.
- app/Controllers/Api/V1/: controladores REST.
- app/Models/: acceso a tablas MySQL.
- app/Entities/: representación de entidades de dominio.
- app/Services/: lógica de negocio reutilizable.
- app/Views/: vistas HTML5 con componentes Bootstrap 5.
- public/assets/: CSS, JS e imágenes.

data-model.md
- users: usuarios autenticados.
- tickets: incidencias registradas.
- ticket_comments: comentarios internos o visibles al usuario.
- ticket_status_history: histórico de cambios de estado.

integrations.md
- GitHub: repositorio fuente y pull requests.
- SFTP: subida al servidor de desarrollo.
- MySQL: persistencia principal.

deployment.md
- Rama develop genera despliegue en servidor de desarrollo.
- Subida por SFTP a /var/www/dev-incidencias/.
- Migraciones ejecutadas con php spark migrate.
```

Si durante el desarrollo se decide cambiar de subida manual por SFTP a GitHub Actions con despliegue automatizado, esa decisión debería registrarse como un ADR, por ejemplo `ADR-001-automatizar-despliegue-desarrollo.md`.

### `spec/api/`

Contiene el contrato OpenAPI.

En proyectos API, este contrato debe mantenerse alineado con el código. Toda feature que añada, modifique o elimine endpoints debe actualizar `spec/api/openapi.yaml` o justificar por qué no aplica.

**Ejemplo aplicado:**

En el **Portal de Incidencias**, `api/openapi.yaml` documentaría los endpoints REST consumidos por el frontend, por integraciones internas o por herramientas externas.

Ejemplo de endpoints documentados:

```text
POST   /api/v1/login
GET    /api/v1/me
GET    /api/v1/tickets
POST   /api/v1/tickets
GET    /api/v1/tickets/{ticketId}
PATCH  /api/v1/tickets/{ticketId}/status
POST   /api/v1/tickets/{ticketId}/comments
```

Ejemplo de regla aplicable:

```text
Si se implementa TicketController::create(), debe existir en openapi.yaml:
- path /api/v1/tickets
- método POST
- requestBody con title, description y priority
- respuestas 201, 400, 401, 403 y 500
- esquema TicketResponse
```

Esto evita que el código de la API evolucione por un lado y la documentación contractual por otro.

### `spec/features/`

Contiene una carpeta por feature.

Cada feature debe documentarse como una unidad trazable, verificable y auditable. El patrón recomendado es:

```text
features/001-login-api/
├── spec.md
├── plan.md
├── tasks.md
├── test-plan.md
├── security-review.md
├── verification.md
├── traceability.md
└── release-notes.md
```

**Ejemplo aplicado:**

En el **Portal de Incidencias**, una feature real podría ser `001-crear-ticket-incidencia`.

Ejemplo de uso:

```text
features/001-crear-ticket-incidencia/spec.md
- El usuario autenticado puede crear una incidencia indicando título, descripción y prioridad.
- El sistema valida campos obligatorios en frontend y backend.
- La incidencia queda registrada en MySQL con estado inicial "abierta".
- El sistema devuelve una respuesta JSON con el identificador del ticket.

features/001-crear-ticket-incidencia/plan.md
- Crear migración para tabla tickets si no existe.
- Crear TicketModel.
- Crear TicketEntity.
- Crear TicketService.
- Crear endpoint POST /api/v1/tickets.
- Crear formulario HTML5 con Bootstrap 5.
- Añadir validaciones en CodeIgniter 4.
- Añadir pruebas PHPUnit.

features/001-crear-ticket-incidencia/tasks.md
- TASK-001: crear migración de tickets.
- TASK-002: crear modelo y entidad.
- TASK-003: crear servicio de alta de incidencia.
- TASK-004: crear endpoint API.
- TASK-005: crear vista Bootstrap 5.
- TASK-006: crear pruebas PHPUnit.
- TASK-007: actualizar openapi.yaml.
```

Esta carpeta permitiría pedir al agente de IA una implementación acotada, con menor riesgo de que modifique partes no relacionadas del proyecto.

### `spec/testing/`

Define la estrategia transversal de pruebas.

Debe indicar tipos de pruebas, herramientas, cobertura mínima, datos de prueba, fixtures, pruebas de integración, pruebas de API, pruebas de regresión y responsabilidades.

**Ejemplo aplicado:**

En el **Portal de Incidencias**, `testing/test-strategy.md` definiría que PHPUnit es la herramienta obligatoria para validar servicios, modelos, controladores y endpoints críticos.

Ejemplo de contenido esperado:

```text
Herramienta principal
- PHPUnit ejecutado con vendor/bin/phpunit.

Base de datos de pruebas
- MySQL con esquema incidencias_test.
- Datos de prueba cargados mediante seeds de CodeIgniter 4.

Tipos de prueba
- Unitarias: TicketServiceTest, UserPermissionServiceTest.
- Modelo: TicketModelTest.
- API/Feature: CreateTicketApiTest, LoginApiTest.
- Validación: campos obligatorios, longitud máxima, prioridad permitida.
- Seguridad: usuario no autenticado, usuario sin permisos, payload inválido.

Comandos mínimos
- composer install
- php spark migrate --all
- php spark db:seed TestSeeder
- vendor/bin/phpunit
```

Para una feature como `001-crear-ticket-incidencia`, el plan de pruebas debería cubrir como mínimo creación correcta, error por falta de autenticación, error por datos inválidos y persistencia correcta en MySQL.

### `spec/operations/`

Define cómo se despliega, observa y revierte el sistema.

Incluye runbook de despliegue, plan de rollback y observabilidad mínima esperada: logs, métricas, trazas, alertas y eventos de auditoría.

**Ejemplo aplicado:**

En el **Portal de Incidencias**, `operations/` documentaría el procedimiento operativo para subir la aplicación al servidor de desarrollo mediante SFTP.

Ejemplo de contenido esperado:

```text
deployment-runbook.md
- Rama origen: develop.
- Repositorio: GitHub.
- Servidor desarrollo: dev.incidencias.example.com.
- Ruta remota: /var/www/dev-incidencias/.
- Método de subida: SFTP.
- Ficheros excluidos: .git/, .env, tests temporales, documentación privada.
- Comando posterior: php spark migrate.
- Verificación posterior: acceder a /health y ejecutar login de prueba.

rollback-plan.md
- Mantener copia de la release anterior en /var/www/dev-incidencias/releases/previous.
- Antes de migrar MySQL, generar backup de la base de datos.
- Si falla el smoke test, restaurar release anterior y backup si aplica.

observability.md
- Revisar writable/logs/ de CodeIgniter 4.
- Registrar errores de API sin exponer datos sensibles.
- Registrar intentos fallidos de login.
- Registrar creación y cambio de estado de tickets.
```

Este bloque evita que el despliegue dependa de memoria personal o instrucciones verbales.

### `spec/risk/`

Contiene el registro de riesgos.

Debe recoger riesgos técnicos, funcionales, operativos, legales y de seguridad, junto con impacto, probabilidad, mitigación, responsable y estado.

**Ejemplo aplicado:**

En el **Portal de Incidencias**, `risk/risk-register.md` recogería riesgos propios de una aplicación PHP desplegada por SFTP, con MySQL y consumo mediante frontend HTML5/Bootstrap 5.

Ejemplo de riesgos:

```text
RISK-001: subida incompleta por SFTP
- Impacto: alto.
- Probabilidad: media.
- Mitigación: checklist de despliegue, comparación de checksums y smoke test posterior.

RISK-002: migración MySQL destructiva
- Impacto: alto.
- Probabilidad: baja/media.
- Mitigación: backup previo, migraciones reversibles y revisión manual antes de ejecutar en desarrollo compartido.

RISK-003: endpoint documentado de forma incompleta
- Impacto: medio.
- Probabilidad: media.
- Mitigación: gate obligatorio de actualización de openapi.yaml.

RISK-004: validación solo en frontend
- Impacto: alto.
- Probabilidad: media.
- Mitigación: duplicar validaciones en CodeIgniter 4 y cubrirlas con PHPUnit.

RISK-005: fuga de credenciales del entorno
- Impacto: crítico.
- Probabilidad: baja/media.
- Mitigación: excluir .env del repositorio GitHub y de paquetes de despliegue, revisar permisos en servidor y no registrar secretos en logs.
```

Este registro debe revisarse cuando una feature introduzca cambios en autenticación, permisos, base de datos, despliegue, API o tratamiento de datos personales.

## ¿Qué documentos se debe tener para rellenar los artefactos?

### 1. Documentos técnicos necesarios para rellenar los artefactos obligatorios

Para los artefactos obligatorios de arranque del proyecto, necesitaría estos documentos de entrada:

| Documento técnico de entrada                                      | Artefactos que permite rellenar                                                       | Contenido mínimo necesario                                                                                                                                                                                                                                                                                                                                                                                                              |
| ----------------------------------------------------------------- | ------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Documento de visión funcional del producto**                    | `spec/constitution/mission.md`                                                        | Qué se construye, para quién, problema que resuelve, propuesta de valor, límites del proyecto, exclusiones y KPIs. El propio `mission.md` pide descripción del producto, usuarios, cliente, equipo técnico, terceros integradores, propuesta de valor, límites e indicadores de éxito.                                                                                                                                                  |
| **Documento de alcance funcional inicial / backlog inicial**      | `spec/constitution/mission.md`, `spec/constitution/roadmap.md`, primera feature       | Features previstas, prioridad, versión objetivo, qué entra en MVP, qué queda fuera, dependencias funcionales y entregas previstas.                                                                                                                                                                                                                                                                                                      |
| **Documento de stack tecnológico y restricciones técnicas**       | `spec/constitution/tech-stack.md`                                                     | Lenguaje, framework, base de datos, servidor HTTP, gestor de dependencias, herramienta de testing, análisis estático, estilo de código, uso o no de contenedores, entornos y comandos reales del proyecto. El template ya espera lenguaje, framework, auth, BD, servidor, Composer, OpenAPI, PHPUnit, PHPStan/Psalm y PSR-12.                                                                                                           |
| **Documento de estándares de desarrollo**                         | `spec/constitution/coding-standards.md`                                               | Convenciones de nombres, tipado, estructura de clases, separación por capas, PHPDoc/JSDoc/JavaDoc según stack, reglas de validación, gestión de errores y estilo de código. El artefacto exige criterios sobre funciones pequeñas, tipado, controladores finos, servicios testeables, documentación de funciones públicas y validación.                                                                                                 |
| **Documento de seguridad base del proyecto**                      | `spec/constitution/security.md`, `quality-gates.md`, `security-review.md` de features | Autenticación, autorización, gestión de sesiones/tokens/API keys, rate limiting, CSRF, CORS, cabeceras de seguridad, clasificación de datos, secretos, logging seguro, OWASP y tratamiento de datos personales. El template contempla autenticación, autorización, APIs multi-cliente, validación, protecciones web/API, datos sensibles, secretos, logging y checklist OWASP.                                                          |
| **Documento de Definition of Ready / Definition of Done técnico** | `spec/constitution/quality-gates.md`                                                  | Condiciones para empezar una feature, condiciones para cerrarla, pruebas mínimas, lint/análisis estático, actualización de OpenAPI, migraciones, seguridad, documentación, verificación y trazabilidad. La plantilla exige `spec.md`, criterios de aceptación, `plan.md`, `tasks.md` e identificación de impactos antes de implementar; y exige tests, OpenAPI, migraciones, seguridad, evidencias, trazabilidad y roadmap para cerrar. |
| **Documento de flujo Git / gestión de ramas / PR**                | `spec/constitution/git-workflow.md`                                                   | Modelo GitFlow o trunk-based, ramas protegidas, formato de ramas, uso de Jira, formato de commits, reglas de PR, CI obligatorio y revisión humana. El template recomienda `main/master`, `develop`, `feature/JIRA-123`, `bugfix`, `hotfix`, `release`, y vinculación con Jira.                                                                                                                                                          |
| **Documento de arquitectura inicial**                             | `spec/architecture/overview.md`                                                       | Tipo de sistema, módulos principales, capas, vista de contexto, dependencias externas, reglas de compatibilidad y límites arquitectónicos. El artefacto pide objetivo arquitectónico, vista de contexto, módulos, dependencias externas y reglas de compatibilidad.                                                                                                                                                                     |
| **Documento de contrato API inicial**                             | `spec/api/openapi.yaml`, `spec/architecture/api-contract.md`                          | Nombre de API, versión, servidores, autenticación, endpoints iniciales, schemas, errores, paginación, versionado, headers y formato común de respuesta. El `openapi.yaml` ya parte de OpenAPI 3.0.3, servidores, tags, `/health`, security schemes y schemas base.                                                                                                                                                                      |
| **Documento de primera feature / especificación funcional**       | `spec/features/NNN-nombre-feature/spec.md`                                            | Estado, Jira, responsable, fecha, versión objetivo, resumen, problema, objetivos, fuera de alcance, actores, historias de usuario, reglas de negocio, criterios de aceptación, impacto API, impacto datos, seguridad, no funcionales, suposiciones y dudas. Todo eso está previsto en el template de `spec.md`.                                                                                                                         |
| **Documento de diseño técnico de la feature**                     | `spec/features/NNN-nombre-feature/plan.md`                                            | Enfoque técnico, módulos afectados, endpoints, validaciones, autorización, modelo de datos, errores, seguridad, pruebas, despliegue, riesgos, decisiones y dudas bloqueantes.                                                                                                                                                                                                                                                           |
| **Documento de desglose de tareas técnicas**                      | `spec/features/NNN-nombre-feature/tasks.md`                                           | Tareas pequeñas, verificables y trazables: contrato, datos, implementación, pruebas, seguridad, calidad, cierre y PR. El template estructura tareas por preparación, contrato/datos, implementación, pruebas, seguridad/calidad y cierre.                                                                                                                                                                                               |
| **Documento de plan de pruebas de feature**                       | `spec/features/NNN-nombre-feature/test-plan.md`                                       | Casos unitarios, integración/API, seguridad, datos de prueba, casos negativos obligatorios y comandos de ejecución.                                                                                                                                                                                                                                                                                                                     |
| **Documento de revisión de seguridad de feature**                 | `spec/features/NNN-nombre-feature/security-review.md`                                 | Superficie de ataque, endpoints, formularios, ficheros, integraciones, datos sensibles, amenazas STRIDE simplificadas, checklist y hallazgos.                                                                                                                                                                                                                                                                                           |

### 2. Documentos necesarios para rellenar el resto de artefactos

Para completar el resto de artefactos de la plantilla, además de los anteriores, necesitaría estos documentos:

| Documento técnico de entrada                     | Artefactos que permite rellenar                                            | Contenido necesario                                                                                                                                                                                                                     |
| ------------------------------------------------ | -------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Modelo de datos / DER / diccionario de datos** | `spec/architecture/data-model.md`                                          | Entidades, tablas, campos, tipos, relaciones, índices, claves, timestamps, soft delete, migraciones, clasificación de datos y sensibilidad. El template pide convenciones, entidades, relaciones, migraciones y clasificación de datos. |
| **Catálogo de integraciones externas**           | `spec/architecture/integrations.md`                                        | Servicios externos, tipo de integración, propietario, datos enviados/recibidos, criticidad, variables `.env`, timeouts, reintentos, fallback y degradación.                                                                             |
| **Documento de arquitectura de despliegue**      | `spec/architecture/deployment.md`, `spec/operations/deployment-runbook.md` | Entornos, URLs, ramas, bases de datos, document root, permisos, TLS, variables, configuración, pasos de despliegue, backups, migraciones, cache, reinicios y smoke tests.                                                               |
| **Runbook operativo de despliegue**              | `spec/operations/deployment-runbook.md`                                    | Precondiciones, release aprobada, CI verde, backup, ventana de mantenimiento, pasos de despliegue, smoke tests y evidencias.                                                                                                            |
| **Plan de rollback / recuperación**              | `spec/operations/rollback-plan.md`, `release-notes.md`                     | Rollback de código, configuración, base de datos, feature flags, versión anterior, backups, migraciones reversibles, responsable y criterios de activación.                                                                             |
| **Documento de observabilidad y auditoría**      | `spec/operations/observability.md`                                         | Logs, correlation ID, métricas, alertas, eventos de auditoría, errores 4xx/5xx, login fallidos, rate limits, latencia e integraciones externas.                                                                                         |
| **Estrategia transversal de pruebas**            | `spec/testing/test-strategy.md`                                            | Niveles de prueba, unitarias, integración, contrato, seguridad, regresión, smoke, datos de prueba, mínimos por feature API y criterios de calidad.                                                                                      |
| **Registro inicial de riesgos**                  | `spec/risk/risk-register.md`                                               | Riesgos técnicos, funcionales, operativos, legales y de seguridad, probabilidad, impacto, severidad, mitigación, responsable y estado. El artefacto exige precisamente esos campos.                                                     |
| **Documento de decisiones arquitectónicas**      | `spec/architecture/decisions/ADR-000-template.md`                          | Contexto, decisión tomada, alternativas consideradas, ventajas, inconvenientes, motivo de descarte, consecuencias e impacto en código, seguridad, operaciones y documentación.                                                          |
| **Glosario funcional/técnico del dominio**       | `spec/constitution/glossary.md`                                            | Términos de negocio, términos técnicos, definiciones, notas y fuentes. El template ya incluye términos como Cliente API, Tenant y Correlation ID.                                                                                       |
| **Política de documentación del proyecto**       | `spec/constitution/documentation.md`                                       | Qué documentos se mantienen vivos, cuándo se actualizan, idioma, normas para README, `.env.example`, OpenAPI, arquitectura y documentación de features.                                                                                 |
| **Roadmap de producto y releases**               | `spec/constitution/roadmap.md`                                             | Features hechas, en curso, siguientes, backlog, descartadas, responsables, bloqueos, fechas y versiones.                                                                                                                                |
| **Evidencias de ejecución y QA**                 | `spec/features/NNN-nombre-feature/verification.md`, `traceability.md`      | Salida de tests, lint, análisis estático, pruebas manuales/API, evidencias, hallazgos, estado de criterios de aceptación, DoD, roadmap y release notes.                                                                                 |
| **Matriz de trazabilidad**                       | `spec/features/NNN-nombre-feature/traceability.md`                         | Relación entre requisitos, criterios de aceptación, tareas, tests, ficheros, endpoints, OpenAPI, migraciones y rollback.                                                                                                                |
| **Notas de release / entrega**                   | `spec/features/NNN-nombre-feature/release-notes.md`                        | Resumen de negocio, cambios técnicos, cambios API, migraciones, variables de entorno, riesgos de despliegue y rollback.                                                                                                                 |






## Flujo recomendado para iniciar un proyecto

1. Copiar la carpeta `spec/` en la raíz del proyecto.
2. Rellenar `spec/constitution/mission.md`.
3. Rellenar `spec/constitution/tech-stack.md`.
4. Definir estándares en `coding-standards.md`.
5. Definir seguridad base en `security.md`.
6. Definir gates obligatorios en `quality-gates.md`.
7. Documentar arquitectura inicial en `architecture/overview.md`.
8. Documentar contrato API inicial en `api/openapi.yaml`.
9. Crear la primera feature en `features/001-nombre-feature/`.
10. Ejecutar `/init` en OpenCode cuando el proyecto ya tenga su estructura real y la carpeta `spec/`.

## Flujo recomendado para una feature

El ejemplo de esta sección usa la feature `001-crear-ticket-incidencia` del **Portal de Incidencias**: una aplicación PHP con **CodeIgniter 4**, repositorio en **GitHub**, subida al servidor de desarrollo por **SFTP**, base de datos **MySQL**, pruebas con **PHPUnit** y frontend **HTML5 + Bootstrap 5**.

### 1. Crear una carpeta nueva en `spec/features/`

La carpeta debe usar numeración incremental y un nombre corto, expresivo y estable.

Ejemplos de nomenclatura:

```text
spec/features/001-crear-ticket-incidencia/
spec/features/002-listar-mis-incidencias/
spec/features/003-cambiar-estado-incidencia/
spec/features/004-comentar-incidencia/
```

Ejemplo real aplicado:

```text
spec/features/001-crear-ticket-incidencia/
├── spec.md
├── plan.md
├── tasks.md
├── test-plan.md
├── security-review.md
├── verification.md
├── traceability.md
└── release-notes.md
```

La carpeta `001-crear-ticket-incidencia` representa una única intención funcional: permitir que un usuario autenticado registre una incidencia desde el portal web o desde la API.

### 2. Escribir `spec.md`

El fichero `spec.md` define qué debe hacer la feature, por qué existe y cómo se validará funcionalmente. No debe describir todavía el detalle técnico de implementación salvo que forme parte de una restricción funcional.

Debe contener, como mínimo, estos campos.

#### Objetivo

Describe la intención funcional de la feature.

Ejemplo:

```text
Permitir que un usuario autenticado cree una nueva incidencia indicando título, descripción y prioridad, quedando registrada en MySQL con estado inicial "abierta" y asociada al usuario creador.
```

#### Alcance

Define qué sí queda incluido.

Ejemplo:

```text
- Crear incidencia desde formulario web HTML5 con Bootstrap 5.
- Crear incidencia mediante endpoint REST POST /api/v1/tickets.
- Validar título, descripción y prioridad en frontend y backend.
- Persistir la incidencia en la tabla tickets de MySQL.
- Asociar la incidencia al usuario autenticado.
- Devolver confirmación visual en frontend y respuesta JSON en API.
```

#### Fuera de alcance

Define qué no debe implementarse en esta feature, aunque esté relacionado.

Ejemplo:

```text
- No se implementa subida de adjuntos.
- No se implementa asignación automática a técnicos.
- No se implementa sistema de SLA.
- No se implementan notificaciones por email.
- No se implementa edición posterior de la incidencia.
- No se implementa borrado lógico ni físico de incidencias.
```

#### Actores

Identifica los usuarios, sistemas o roles implicados.

Ejemplo:

```text
- Usuario autenticado: crea la incidencia.
- Técnico de soporte: no interviene en esta feature, pero será consumidor posterior de la incidencia.
- Administrador: no interviene en esta feature.
- Sistema: valida, registra y devuelve el resultado de la operación.
```

#### Requisitos funcionales

Deben ser numerados y verificables.

Ejemplo:

```text
REQ-001: El usuario autenticado puede acceder al formulario de creación de incidencia.
REQ-002: El formulario debe solicitar título, descripción y prioridad.
REQ-003: El sistema debe aceptar únicamente las prioridades baja, media y alta.
REQ-004: Al enviar datos válidos, el sistema debe crear un registro en la tabla tickets.
REQ-005: La incidencia debe quedar asociada al identificador del usuario autenticado.
REQ-006: La incidencia debe crearse con estado inicial abierta.
REQ-007: El endpoint POST /api/v1/tickets debe devolver HTTP 201 cuando la incidencia se crea correctamente.
REQ-008: El endpoint debe devolver HTTP 400 cuando el payload sea inválido.
REQ-009: El endpoint debe devolver HTTP 401 cuando el usuario no esté autenticado.
```

#### Requisitos no funcionales

Deben indicar restricciones de seguridad, rendimiento, mantenibilidad, compatibilidad o calidad.

Ejemplo:

```text
NFR-001: La feature debe implementarse en PHP 8.x usando CodeIgniter 4.
NFR-002: Las validaciones backend deben implementarse con los mecanismos de validación de CodeIgniter 4.
NFR-003: El formulario debe ser HTML5 válido y usar componentes Bootstrap 5.
NFR-004: La creación de la incidencia debe completarse en menos de 500 ms en entorno de desarrollo con MySQL local o equivalente.
NFR-005: La feature debe cubrirse con pruebas PHPUnit.
NFR-006: No se deben registrar en logs datos sensibles ni contenido completo de la descripción.
NFR-007: El endpoint debe estar documentado en spec/api/openapi.yaml.
```

#### Criterios de aceptación

Deben expresar condiciones observables para aceptar o rechazar la feature.

Ejemplo:

```text
AC-001: Dado un usuario autenticado, cuando accede a /tickets/new, entonces ve un formulario con título, descripción y prioridad.
AC-002: Dado un usuario autenticado, cuando envía el formulario con datos válidos, entonces se crea una incidencia en MySQL con estado abierta.
AC-003: Dado un usuario autenticado, cuando envía el formulario sin título, entonces se muestra un mensaje de validación y no se crea la incidencia.
AC-004: Dado un cliente API autenticado, cuando envía POST /api/v1/tickets con payload válido, entonces recibe HTTP 201 y el identificador del ticket creado.
AC-005: Dado un cliente API no autenticado, cuando envía POST /api/v1/tickets, entonces recibe HTTP 401.
AC-006: Dado un cliente API autenticado, cuando envía una prioridad no permitida, entonces recibe HTTP 400.
AC-007: La ejecución de vendor/bin/phpunit debe finalizar sin errores.
AC-008: spec/api/openapi.yaml debe incluir el endpoint POST /api/v1/tickets con request, responses y esquema de salida.
```

### 3. Escribir `plan.md`

El fichero `plan.md` define cómo se implementará la feature. Debe traducir la intención de `spec.md` a decisiones técnicas concretas.

Debe contener, como mínimo, estos campos.

#### Enfoque técnico

Describe la estrategia de implementación.

Ejemplo:

```text
La feature se implementará siguiendo el patrón MVC de CodeIgniter 4. Se añadirá un controlador web para mostrar y procesar el formulario HTML5/Bootstrap 5, un controlador API para aceptar POST /api/v1/tickets, un servicio TicketService para centralizar la lógica de creación, un modelo TicketModel para persistencia MySQL y una entidad TicketEntity para representar la incidencia.

La validación se aplicará en dos capas: restricciones HTML5 en frontend para mejorar UX y validación obligatoria backend en CodeIgniter 4 como control real de seguridad.
```

#### Archivos afectados

Lista los ficheros que se prevé crear o modificar.

Ejemplo:

```text
app/Controllers/Web/TicketController.php
app/Controllers/Api/V1/TicketController.php
app/Models/TicketModel.php
app/Entities/TicketEntity.php
app/Services/TicketService.php
app/Database/Migrations/2026-06-27-000001_CreateTicketsTable.php
app/Views/tickets/new.php
app/Views/tickets/created.php
app/Config/Routes.php
tests/unit/Services/TicketServiceTest.php
tests/feature/Api/CreateTicketApiTest.php
spec/api/openapi.yaml
```

#### Endpoints

Documenta los endpoints afectados.

Ejemplo:

```text
POST /api/v1/tickets

Request JSON:
{
  "title": "No puedo acceder al panel",
  "description": "Al iniciar sesión aparece un error 500.",
  "priority": "alta"
}

Response 201:
{
  "id": 123,
  "title": "No puedo acceder al panel",
  "priority": "alta",
  "status": "abierta",
  "createdAt": "2026-06-27T10:30:00+00:00"
}

Response 400:
{
  "error": "validation_error",
  "fields": {
    "title": "El título es obligatorio."
  }
}
```

Rutas web asociadas:

```text
GET  /tickets/new
POST /tickets
```

#### Modelo de datos

Define tablas, campos, relaciones e índices.

Ejemplo:

```text
Tabla: tickets

Campos:
- id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY
- user_id BIGINT UNSIGNED NOT NULL
- title VARCHAR(150) NOT NULL
- description TEXT NOT NULL
- priority ENUM('baja', 'media', 'alta') NOT NULL DEFAULT 'media'
- status ENUM('abierta', 'en_progreso', 'resuelta', 'cerrada') NOT NULL DEFAULT 'abierta'
- created_at DATETIME NOT NULL
- updated_at DATETIME NULL
- deleted_at DATETIME NULL

Índices:
- INDEX idx_tickets_user_id (user_id)
- INDEX idx_tickets_status (status)
- INDEX idx_tickets_priority (priority)

Relaciones:
- tickets.user_id referencia al usuario creador.
```

#### Servicios

Define la lógica de negocio que no debe quedar incrustada en controladores.

Ejemplo:

```text
TicketService::createTicket(int $userId, array $payload): TicketEntity

Responsabilidades:
- Normalizar datos de entrada.
- Validar que la prioridad pertenece al catálogo permitido.
- Crear la entidad TicketEntity.
- Persistir mediante TicketModel.
- Devolver la entidad creada.

No debe:
- Leer directamente $_POST.
- Renderizar vistas.
- Construir respuestas HTTP.
- Ejecutar consultas SQL manuales fuera de TicketModel.
```

#### Validaciones

Define reglas frontend y backend.

Ejemplo:

```text
Frontend HTML5:
- title: required, maxlength="150"
- description: required, minlength="10"
- priority: select obligatorio con valores baja, media, alta

Backend CodeIgniter 4:
- title: required|min_length[5]|max_length[150]
- description: required|min_length[10]|max_length[5000]
- priority: required|in_list[baja,media,alta]

Normalización:
- title: trim.
- description: trim.
- priority: lowercase.
```

#### Migraciones

Define los cambios de base de datos.

Ejemplo:

```text
Crear migración:
app/Database/Migrations/2026-06-27-000001_CreateTicketsTable.php

Comando de aplicación:
php spark migrate

Comando de reversión en desarrollo:
php spark migrate:rollback

Consideraciones:
- La migración no debe destruir datos existentes.
- Si la tabla tickets ya existe, revisar compatibilidad antes de aplicar.
- El rollback solo se ejecutará en desarrollo si no hay datos relevantes.
```

#### Riesgos técnicos

Identifica riesgos de implementación antes de tocar código.

Ejemplo:

```text
RISK-001: duplicar lógica de validación entre controlador web y controlador API.
Mitigación: centralizar reglas en TicketValidationRules o método privado reutilizable.

RISK-002: crear incidencia sin usuario autenticado por error de control de sesión.
Mitigación: aplicar filtro de autenticación en rutas web y API.

RISK-003: divergencia entre implementación y OpenAPI.
Mitigación: actualizar spec/api/openapi.yaml en la misma tarea que el endpoint.

RISK-004: subida SFTP incompleta al servidor de desarrollo.
Mitigación: checklist de despliegue y smoke test posterior.
```

### 4. Escribir `tasks.md`

El fichero `tasks.md` convierte el plan en trabajo ejecutable. Las tareas deben ser pequeñas, verificables y vinculadas a requisitos o criterios de aceptación.

Debe contener, como mínimo, estos campos.

#### Tareas pequeñas

Ejemplo:

```text
TASK-001: Crear migración MySQL para tabla tickets.
TASK-002: Crear TicketEntity.
TASK-003: Crear TicketModel.
TASK-004: Crear TicketService::createTicket().
TASK-005: Crear controlador API app/Controllers/Api/V1/TicketController.php.
TASK-006: Crear rutas API en app/Config/Routes.php.
TASK-007: Crear controlador web app/Controllers/Web/TicketController.php.
TASK-008: Crear vista app/Views/tickets/new.php con HTML5 y Bootstrap 5.
TASK-009: Añadir validaciones frontend HTML5.
TASK-010: Añadir validaciones backend CodeIgniter 4.
TASK-011: Crear tests PHPUnit unitarios de TicketService.
TASK-012: Crear tests PHPUnit de endpoint POST /api/v1/tickets.
TASK-013: Actualizar spec/api/openapi.yaml.
TASK-014: Ejecutar pruebas y documentar resultados en verification.md.
```

#### Verificables

Cada tarea debe indicar cómo se comprueba.

Ejemplo:

```text
TASK-001 se verifica ejecutando php spark migrate y comprobando que existe la tabla tickets en MySQL.
TASK-004 se verifica con tests unitarios de TicketService.
TASK-005 se verifica con test de API CreateTicketApiTest.
TASK-008 se verifica accediendo a /tickets/new en servidor de desarrollo.
TASK-013 se verifica revisando que openapi.yaml contiene POST /api/v1/tickets.
```

#### Marcables como completadas

Ejemplo:

```text
- [x] TASK-001: Crear migración MySQL para tabla tickets.
- [x] TASK-002: Crear TicketEntity.
- [x] TASK-003: Crear TicketModel.
- [ ] TASK-004: Crear TicketService::createTicket().
- [ ] TASK-005: Crear controlador API.
- [ ] TASK-006: Crear rutas API.
- [ ] TASK-007: Crear controlador web.
- [ ] TASK-008: Crear vista Bootstrap 5.
- [ ] TASK-009: Añadir validaciones frontend.
- [ ] TASK-010: Añadir validaciones backend.
- [ ] TASK-011: Crear tests unitarios.
- [ ] TASK-012: Crear tests de API.
- [ ] TASK-013: Actualizar OpenAPI.
- [ ] TASK-014: Completar verification.md.
```

#### Asociables a requisitos y criterios de aceptación

Ejemplo:

```text
TASK-001 -> REQ-004, REQ-006, AC-002
TASK-004 -> REQ-004, REQ-005, REQ-006, AC-002
TASK-005 -> REQ-007, REQ-008, REQ-009, AC-004, AC-005, AC-006
TASK-008 -> REQ-001, REQ-002, AC-001
TASK-010 -> REQ-003, AC-003, AC-006
TASK-011 -> NFR-005, AC-007
TASK-013 -> NFR-007, AC-008
```

### 5. Escribir `test-plan.md`

El fichero `test-plan.md` define cómo se validará la feature antes de cerrarla.

Debe contener, como mínimo, estos campos.

#### Tests unitarios

Ejemplo:

```text
TicketServiceTest::testCreateTicketWithValidPayloadCreatesTicket()
- Valida que TicketService crea una incidencia con datos válidos.

TicketServiceTest::testCreateTicketNormalizesPayload()
- Valida trim de título y descripción.
- Valida normalización lowercase de prioridad.

TicketServiceTest::testCreateTicketRejectsInvalidPriority()
- Valida que una prioridad fuera de catálogo no se acepta.
```

#### Tests de integración

Ejemplo:

```text
TicketModelTest::testTicketIsPersistedInMysql()
- Inserta una incidencia en la base de datos de pruebas MySQL.
- Comprueba que user_id, title, priority y status se guardan correctamente.

TicketMigrationTest::testTicketsTableExists()
- Comprueba que la migración crea la tabla tickets con los campos esperados.
```

#### Tests de API

Ejemplo:

```text
CreateTicketApiTest::testAuthenticatedUserCanCreateTicket()
- POST /api/v1/tickets con token/sesión válida.
- Espera HTTP 201.
- Espera JSON con id, title, priority, status y createdAt.

CreateTicketApiTest::testUnauthenticatedUserCannotCreateTicket()
- POST /api/v1/tickets sin autenticación.
- Espera HTTP 401.

CreateTicketApiTest::testInvalidPayloadReturnsValidationError()
- POST /api/v1/tickets sin title.
- Espera HTTP 400.
- Espera estructura JSON de errores por campo.
```

#### Casos negativos

Ejemplo:

```text
- title vacío: debe fallar.
- title superior a 150 caracteres: debe fallar.
- description inferior a 10 caracteres: debe fallar.
- priority = urgente: debe fallar.
- usuario no autenticado: debe fallar.
- payload JSON malformado: debe fallar sin error 500.
```

#### Casos de seguridad

Ejemplo:

```text
- Intento de crear ticket sin sesión activa.
- Intento de enviar HTML o JavaScript en title.
- Intento de enviar payload con user_id manipulando el propietario.
- Intento de superar longitud máxima en campos.
- Validación de que no se escribe la descripción completa en logs.
```

#### Datos de prueba

Ejemplo:

```text
Usuario autenticado:
- id: 10
- email: usuario.demo@example.com
- rol: user

Payload válido:
{
  "title": "No puedo acceder al panel",
  "description": "Al iniciar sesión aparece un error 500.",
  "priority": "alta"
}

Payload inválido:
{
  "title": "",
  "description": "Error",
  "priority": "urgente"
}

Base de datos:
- Esquema: incidencias_test
- Seeds: UserSeeder, TicketSeeder opcional
```

### 6. Completar `security-review.md`

El fichero `security-review.md` documenta la revisión de seguridad específica de la feature.

Debe contener, como mínimo, estos campos.

#### Autenticación

Ejemplo:

```text
SEC-001: Las rutas GET /tickets/new y POST /tickets requieren usuario autenticado.
SEC-002: El endpoint POST /api/v1/tickets requiere autenticación API o sesión válida según la estrategia definida en constitution/security.md.
SEC-003: Si no existe usuario autenticado, la API devuelve HTTP 401 y la web redirige a login.
```

#### Autorización

Ejemplo:

```text
SEC-004: Un usuario solo puede crear incidencias en su propio nombre.
SEC-005: El backend ignora cualquier user_id recibido en el payload.
SEC-006: El user_id se obtiene exclusivamente desde la sesión o contexto autenticado.
```

#### Validación de entrada

Ejemplo:

```text
SEC-007: title se valida como obligatorio, longitud 5-150 y texto plano.
SEC-008: description se valida como obligatoria, longitud 10-5000.
SEC-009: priority se valida mediante lista cerrada: baja, media, alta.
SEC-010: Los campos no reconocidos del payload no deben modificar propiedades internas.
```

#### Gestión de errores

Ejemplo:

```text
SEC-011: Los errores de validación devuelven HTTP 400 sin stack trace.
SEC-012: Los errores de autenticación devuelven HTTP 401.
SEC-013: Los errores internos devuelven mensaje genérico.
SEC-014: Los logs técnicos no deben incluir secretos, cookies, tokens ni descripciones completas de incidencias.
```

#### Rate limiting

Ejemplo:

```text
SEC-015: POST /api/v1/tickets debe quedar protegido por rate limiting si la API queda expuesta fuera de la red interna.
SEC-016: Límite inicial recomendado: 30 creaciones por usuario cada 10 minutos en desarrollo/preproducción.
SEC-017: Los excesos devuelven HTTP 429.
```

#### CSRF/CORS si aplica

Ejemplo:

```text
SEC-018: El formulario web POST /tickets debe usar protección CSRF de CodeIgniter 4.
SEC-019: El endpoint API no debe depender de CSRF si usa autenticación por token y no por cookie de navegador.
SEC-020: CORS debe permitir únicamente los orígenes definidos en .env para entorno de desarrollo.
```

#### Tratamiento de datos sensibles

Ejemplo:

```text
SEC-021: La descripción de la incidencia puede contener información sensible introducida por el usuario.
SEC-022: No se debe registrar description completa en logs.
SEC-023: No se debe exponer información de otros usuarios en respuestas API.
SEC-024: Los datos se almacenan en MySQL conforme a la política de retención del proyecto.
```

#### Riesgos OWASP

Ejemplo:

```text
API1 Broken Object Level Authorization:
- Riesgo: manipulación de user_id para crear incidencias asociadas a otro usuario.
- Control: user_id siempre se toma del contexto autenticado.

API3 Broken Object Property Level Authorization:
- Riesgo: asignación masiva de campos no permitidos.
- Control: allowlist estricta de title, description y priority.

API4 Unrestricted Resource Consumption:
- Riesgo: creación masiva de tickets.
- Control: rate limiting.

API8 Security Misconfiguration:
- Riesgo: CORS permisivo o errores con stack trace.
- Control: configuración por entorno y errores genéricos en producción.

XSS:
- Riesgo: title o description con HTML/JavaScript.
- Control: escape en vistas y validación/sanitización adecuada.
```

### 7. Mantener `traceability.md`

El fichero `traceability.md` permite auditar qué requisito queda cubierto por qué tarea, qué prueba y qué evidencia.

Debe contener, como mínimo, estos campos.

#### Requisito

Ejemplo:

```text
REQ-004: Al enviar datos válidos, el sistema debe crear un registro en la tabla tickets.
```

#### Criterio de aceptación

Ejemplo:

```text
AC-002: Dado un usuario autenticado, cuando envía el formulario con datos válidos, entonces se crea una incidencia en MySQL con estado abierta.
AC-004: Dado un cliente API autenticado, cuando envía POST /api/v1/tickets con payload válido, entonces recibe HTTP 201 y el identificador del ticket creado.
```

#### Tarea

Ejemplo:

```text
TASK-001: Crear migración MySQL para tabla tickets.
TASK-003: Crear TicketModel.
TASK-004: Crear TicketService::createTicket().
TASK-005: Crear controlador API.
```

#### Test

Ejemplo:

```text
TEST-001: TicketServiceTest::testCreateTicketWithValidPayloadCreatesTicket()
TEST-004: CreateTicketApiTest::testAuthenticatedUserCanCreateTicket()
TEST-005: TicketModelTest::testTicketIsPersistedInMysql()
```

#### Evidencia

Ejemplo:

```text
EVID-001: Captura o salida de vendor/bin/phpunit con resultado OK.
EVID-002: Registro creado en tabla tickets del esquema incidencias_test.
EVID-003: Respuesta HTTP 201 de POST /api/v1/tickets en entorno de desarrollo.
EVID-004: Revisión de spec/api/openapi.yaml con path documentado.
```

Ejemplo de tabla de trazabilidad:

```text
| Requisito | Criterio | Tarea | Test | Evidencia |
|-----------|----------|-------|------|-----------|
| REQ-004 | AC-002, AC-004 | TASK-001, TASK-003, TASK-004, TASK-005 | TEST-001, TEST-004, TEST-005 | EVID-001, EVID-002, EVID-003 |
| REQ-003 | AC-006 | TASK-010 | TEST-003, TEST-006 | EVID-001 |
| NFR-007 | AC-008 | TASK-013 | Revisión documental | EVID-004 |
```

### 8. Implementar el código

La implementación debe hacerse después de completar `spec.md`, `plan.md`, `tasks.md`, `test-plan.md` y `security-review.md`.

Ejemplo real de ejecución:

```text
Rama GitHub:
feature/JIRA-123-crear-ticket-incidencia

Orden recomendado:
1. Crear migración MySQL.
2. Crear entidad, modelo y servicio.
3. Crear tests unitarios de servicio.
4. Crear controlador API y tests de API.
5. Crear controlador web y vista HTML5/Bootstrap 5.
6. Actualizar rutas.
7. Actualizar OpenAPI.
8. Ejecutar PHPUnit.
9. Subir rama a GitHub.
10. Abrir Pull Request hacia develop.
11. Desplegar en servidor de desarrollo por SFTP tras revisión o aprobación.
```

Regla operativa:

```text
No se debe implementar una tarea que no esté descrita en tasks.md.
Si durante la implementación aparece una necesidad nueva, primero se actualiza spec/ y después se modifica el código.
```

### 9. Completar `verification.md`

El fichero `verification.md` documenta cómo se ha comprobado que la feature cumple la especificación.

Debe contener, como mínimo, estos campos.

#### Comandos ejecutados

Ejemplo:

```text
composer install
php spark migrate --all
php spark db:seed TestSeeder
vendor/bin/phpunit
php spark serve --host 0.0.0.0 --port 8080
```

Comprobación manual en servidor de desarrollo tras subida SFTP:

```text
URL: https://dev.incidencias.example.com/tickets/new
Acción: crear incidencia con usuario demo.
Resultado esperado: mensaje de confirmación y ticket visible en listado.
```

#### Resultado de tests

Ejemplo:

```text
PHPUnit 11.x
Tests: 18
Assertions: 64
Failures: 0
Errors: 0
Skipped: 0
Resultado: OK
```

#### Resultado de lint

Ejemplo:

```text
php -l app/Services/TicketService.php: No syntax errors detected
php -l app/Controllers/Api/V1/TicketController.php: No syntax errors detected
php -l app/Controllers/Web/TicketController.php: No syntax errors detected
php -l app/Models/TicketModel.php: No syntax errors detected
Resultado: OK
```

#### Resultado de análisis estático

Ejemplo:

```text
Herramienta: PHPStan o Psalm, si el proyecto la tiene configurada.
Comando: vendor/bin/phpstan analyse app tests
Resultado: sin errores de nivel configurado.

Si el proyecto todavía no tiene análisis estático:
Resultado: No aplica en esta versión.
Acción pendiente: registrar incorporación de PHPStan/Psalm en roadmap técnico.
```

#### Evidencias

Ejemplo:

```text
EVID-001: salida completa de vendor/bin/phpunit almacenada en verification.md.
EVID-002: captura o registro de respuesta HTTP 201 de POST /api/v1/tickets.
EVID-003: comprobación en MySQL de registro creado en tickets.
EVID-004: revisión de formulario /tickets/new en servidor de desarrollo.
EVID-005: Pull Request en GitHub: feature/JIRA-123-crear-ticket-incidencia -> develop.
EVID-006: subida SFTP completada en /var/www/dev-incidencias/.
```

#### Incidencias detectadas

Ejemplo:

```text
INC-001: El formulario web permitía enviar descripción inferior a 10 caracteres.
Estado: corregido.
Acción: añadido minlength="10" en HTML5 y regla min_length[10] en backend.

INC-002: openapi.yaml no incluía respuesta 401.
Estado: corregido.
Acción: añadida respuesta 401 al endpoint POST /api/v1/tickets.
```

### 10. Completar `release-notes.md` si la feature llega a entrega

El fichero `release-notes.md` resume el cambio en lenguaje comprensible para revisión, despliegue o entrega.

Ejemplo:

```text
# Release notes — 001-crear-ticket-incidencia

## Resumen

Se añade la capacidad de crear incidencias desde el portal web y desde la API REST.

## Cambios funcionales

- Nuevo formulario web /tickets/new con HTML5 y Bootstrap 5.
- Nuevo endpoint POST /api/v1/tickets.
- Creación de incidencias con estado inicial abierta.
- Validación de título, descripción y prioridad.

## Cambios técnicos

- Nueva tabla MySQL tickets.
- Nuevo TicketModel.
- Nuevo TicketEntity.
- Nuevo TicketService.
- Nuevos controladores Web y API.
- Nuevas pruebas PHPUnit.
- Contrato OpenAPI actualizado.

## Seguridad

- Requiere usuario autenticado.
- user_id se obtiene del contexto autenticado, no del payload.
- Validación backend obligatoria.
- Protección CSRF en formulario web.
- Rate limiting previsto para API expuesta.

## Despliegue

- Rama GitHub: feature/JIRA-123-crear-ticket-incidencia.
- Destino inicial: servidor de desarrollo.
- Método: SFTP.
- Requiere ejecutar php spark migrate.

## Rollback

- Revertir Pull Request o commit en rama develop.
- Restaurar versión anterior por SFTP.
- Ejecutar php spark migrate:rollback solo si se confirma que no hay datos relevantes que conservar en desarrollo.

## Verificación

- PHPUnit completado sin errores.
- Smoke test web completado.
- Smoke test API completado.
- OpenAPI revisado.
```

## Convención de trazabilidad

Se recomienda usar identificadores estables:

```text
REQ-001    Requisito funcional
NFR-001    Requisito no funcional
AC-001     Criterio de aceptación
TASK-001   Tarea técnica
TEST-001   Caso de prueba
SEC-001    Control de seguridad
RISK-001   Riesgo
ADR-001    Decisión de arquitectura
```

Ejemplo:

```text
REQ-001 -> AC-001 -> TASK-003 -> TEST-002 -> verification.md
```

Esta trazabilidad permite auditar si el código implementado responde realmente a la intención documentada.

## Uso con OpenCode

El orden recomendado es:

1. Incorporar `spec/` al proyecto.
2. Rellenar como mínimo `mission.md`, `tech-stack.md`, `security.md` y `quality-gates.md`.
3. Añadir o mantener el código real del proyecto.
4. Ejecutar `/init`.
5. Revisar el `AGENTS.md` generado por OpenCode.
6. Ajustar manualmente `AGENTS.md` solo si alguna regla crítica no ha sido inferida correctamente.

Reglas operativas recomendadas:

- Para tareas no triviales, usar modo Plan antes de permitir cambios.
- No pedir implementación directa sin `spec.md`.
- No aceptar cambios que no actualicen tests o verificación.
- No cerrar una feature sin `verification.md`.
- No modificar endpoints sin revisar `openapi.yaml`.
- No aceptar excepciones de seguridad sin registrarlas en `security-review.md` o en un ADR.

## Definition of Done técnica

Una feature se considera terminada únicamente cuando cumple, como mínimo, estos puntos:

- `spec.md` completado.
- `plan.md` completado.
- `tasks.md` completado.
- `test-plan.md` completado.
- `security-review.md` completado.
- `traceability.md` actualizado.
- Código implementado.
- Tests ejecutados y superados.
- Lint y análisis estático ejecutados.
- OpenAPI actualizado si aplica.
- Migraciones documentadas si aplica.
- `verification.md` completado con evidencias.
- `release-notes.md` completado si aplica.
- `roadmap.md` actualizado.

## Reglas de mantenimiento

La plantilla debe tratarse como documentación viva.

No debe convertirse en documentación decorativa. Si el código cambia y la especificación no, la especificación queda obsoleta. Si la especificación cambia y el código no, la implementación queda incompleta.

La regla base es:

```text
Toda decisión relevante debe quedar reflejada en spec/.
```

## Qué no es esta plantilla

Esta plantilla no es:

- Un framework PHP.
- Un generador de código.
- Una estructura MVC.
- Una configuración de OpenCode.
- Un sustituto de tests.
- Un sustituto de revisión humana.
- Un documento comercial.

Es una estructura de control técnico para dirigir el desarrollo con especificaciones, agentes de IA y validación humana.

## Uso recomendado

Esta plantilla es especialmente útil para:

- APIs REST.
- Backends PHP.
- Aplicaciones CodeIgniter 4.
- Integraciones con terceros.
- Sistemas con requisitos de seguridad.
- Proyectos con GitFlow y Jira.
- Equipos que trabajan con agentes de IA.
- Proyectos donde la trazabilidad técnica importa.

También puede adaptarse a otros stacks si se modifican `tech-stack.md`, `coding-standards.md`, `quality-gates.md` y `security.md`.

## Licencia y adaptación

La plantilla está pensada para ser copiada, modificada y adaptada por proyecto.

Antes de usarla en producción, revisa todas las secciones marcadas como plantilla y elimina ejemplos que no apliquen al proyecto real.
