# Estandares de codigo

## Principios

- Codigo claro antes que codigo ingenioso.
- Tipado explicito siempre que sea viable.
- Funciones pequenas, con una responsabilidad principal.
- Controladores finos y servicios testeables.
- Reglas de negocio separadas de la capa HTTP.

## PHP

- Usar `declare(strict_types=1);` cuando el framework y el modulo lo permitan.
- Tipar parametros y retornos en metodos nuevos.
- Evitar propiedades dinamicas.
- Evitar variables genericas como `$data` salvo en contextos acotados.
- Evitar arrays asociativos profundos si un DTO o Entity aporta claridad.
- Usar excepciones especificas para errores de dominio.

## Documentacion de funciones publicas

Cada funcion publica relevante debe incluir PHPDoc con:

- Nombre/resumen.
- Descripcion funcional.
- Alcance.
- Parametros de entrada.
- Valor de salida.
- Excepciones esperadas.
- Autor o equipo responsable si el proyecto lo exige.
- Fecha de ultima actualizacion si el proyecto lo exige.

Ejemplo:

```php
/**
 * Valida y registra una solicitud de login API.
 *
 * Alcance: endpoint publico de autenticacion.
 *
 * @param LoginRequestDto $request Datos validados del login.
 * @return LoginResultDto Resultado autenticado con token y expiracion.
 * @throws InvalidCredentialsException Cuando las credenciales no son validas.
 */
public function login(LoginRequestDto $request): LoginResultDto
{
    // ...
}
```

## Validacion

- Validar formato, tipo, longitud y rango.
- Usar regex solo cuando sea necesario y documentar el patron.
- Validar en frontend para UX, y siempre en backend por seguridad.
- Normalizar entradas antes de usarlas.

## Errores

- Errores API en formato comun.
- No filtrar stack traces.
- No revelar existencia de usuarios en flujos sensibles.
- Registrar correlation ID si existe.
