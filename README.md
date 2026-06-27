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
**Versión de la plantilla:** 1.0.1  
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

1. Crear una carpeta nueva en `spec/features/` usando numeración incremental:
   - `001-login-api`
   - `002-registro-usuario`
   - `003-recuperacion-password`

2. Escribir `spec.md`:
   - Objetivo.
   - Alcance.
   - Fuera de alcance.
   - Actores.
   - Requisitos funcionales.
   - Requisitos no funcionales.
   - Criterios de aceptación.

3. Escribir `plan.md`:
   - Enfoque técnico.
   - Archivos afectados.
   - Endpoints.
   - Modelo de datos.
   - Servicios.
   - Validaciones.
   - Migraciones.
   - Riesgos técnicos.

4. Escribir `tasks.md`:
   - Tareas pequeñas.
   - Verificables.
   - Marcables como completadas.
   - Asociables a requisitos y criterios de aceptación.

5. Escribir `test-plan.md`:
   - Tests unitarios.
   - Tests de integración.
   - Tests de API.
   - Casos negativos.
   - Casos de seguridad.
   - Datos de prueba.

6. Completar `security-review.md`:
   - Autenticación.
   - Autorización.
   - Validación de entrada.
   - Gestión de errores.
   - Rate limiting.
   - CSRF/CORS si aplica.
   - Tratamiento de datos sensibles.
   - Riesgos OWASP.

7. Mantener `traceability.md`:
   - Requisito.
   - Criterio de aceptación.
   - Tarea.
   - Test.
   - Evidencia.

8. Implementar el código.

9. Completar `verification.md`:
   - Comandos ejecutados.
   - Resultado de tests.
   - Resultado de lint.
   - Resultado de análisis estático.
   - Evidencias.
   - Incidencias detectadas.

10. Completar `release-notes.md` si la feature llega a entrega.

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
