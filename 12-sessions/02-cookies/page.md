---
title: Almacenamiento de Sesión en Cookies
status: live
---

Puedes utilizar el middleware `\Slim\Middleware\SessionCookie` para mantener datos 
de sesión en cookies HTTP encriptadas y hasheadas. Para activar el middleware de 
cookies de sesión, añade el middleware `\Slim\Middleware\SessionCookie` a tu aplicación 
Slim:

    <?php
    $app = new Slim();
    $app->add(new \Slim\Middleware\SessionCookie(array(
        'expires' => '20 minutes',
        'path' => '/',
        'domain' => null,
        'secure' => false,
        'httponly' => false,
        'name' => 'slim_session',
        'secret' => 'CAMBIA_ME',
        'cipher' => MCRYPT_RIJNDAEL_256,
        'cipher_mode' => MCRYPT_MODE_CBC
    )));

El segundo parámetro es opcional; lo mostramos aquí para que puedas ver los ajustes 
por defecto del middleware. The session cookie
middleware will work seamlessly with the `$_SESSION` superglobal so you can easily migrate to this session storage
middleware with zero changes to your application code.

If you use the session cookie middleware, you DO NOT need to start a native PHP session. The `$_SESSION` superglobal
will still be available, and it will be persisted into an HTTP cookie via the middleware layer rather than with
PHP’s native session management.

Remember, HTTP cookies are inherently limited to only 4 kilobytes of data. If your encrypted session data will exceed
this length, you should instead rely on PHP’s native sessions or an alternate session store.

<div class="alert">
    <strong>PLEASE NOTE:</strong> Client-side storage of session data is not recommended if you are
    dealing with sensitive information, even when using Slim's encrpyted session cookie middleware.
    If you need to store sensitive information, you should encrypt and store the session information
    on your server.
</div>
