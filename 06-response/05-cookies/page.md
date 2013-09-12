---
title: Cookies de respuesta
status: live
---

La aplicación Slim facilita métods de ayuda para enviar cookies junto con la 
respuesta HTTP.
ci
### Asignar una Cookie

Este ejemplo muestra como utilizar el método `setCookie()` de la aplicación Slim 
para crear una cookie HTTP que enviar junto con la respuesta HTTP:

    <?php
    $app->setCookie('foo', 'bar', '2 days');

Esto crea una cookie HTTP con el nombre "foo" y el valor "bar" que expirará en 
dos días desde ahora. Puedes también indicar propiedades adicionales de estas
cookies, incluyendo ruta, dominio, seguridad y configuración httponly. El 
método `setCookie()` de la aplicación Slim utiliza los mismos parámetros que 
la función nativa de PHP `setCookie()`.

    <?php
    $app->setCookie(
        $name,
        $value,
        $expiresAt,
        $path,
        $domain,
        $secure,
        $httponly
    );

### Asignar una Cookie Encriptada

Puedes indicar a Slim que quieres encriptar las cookies de respuesta 
ajustando la configuración de la aplicación `cookies.encrypt` a `true`.b
Cuando este valor de configuración es `true`, Slim encriptará las cookies
de respuesta automáticamente antes de que sean devueltas al cliente HTTP.

Estos son los valores configurables en la apli´cación Slim utilizados para la 
encriptación de cookies:

    <?php
    $app = new \Slim\Slim(array(
        'cookies.encrypt' => true,
        'cookies.secret_key' => 'my_secret_key',
        'cookies.cipher' => MCRYPT_RIJNDAEL_256,
        'cookies.cipher_mode' => MCRYPT_MODE_CBC
    ));

### Eliminar una Cookie

Puedes eliminar una cookie utilizando el método de la aplicación Slim 
`deleteCookie()`. Esto eliminará la cookie del cliente HTTP antes de la 
próxima petición HTTP. Este método acepta los mismos parámetros que el método 
de la aplicación Slim `setCookie()`, *sin* el parámetro `$expires`. Solo el 
primer parámetro es obligatorio.

    <?php
    $app->deleteCookie('foo');

Si también deseas especificar la ruta y el dominio:

    <?php
    $app->deleteCookie('foo', '/', 'foo.com');

También podrías especificar las propiedades secure y httponly:

    <?php
    $app->deleteCookie('foo', '/', 'foo.com', true, true);
