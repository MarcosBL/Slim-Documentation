---
title: Opciones de la Aplicación
status: live
---

### mode

Este es un identificador para el modo actual de operación de la aplicación. El modo no afecta 
la funcionalidad interna de una aplicación Slim. El modo es solo usado opcionalmente para 
invocar tu propio código con un modo especifico usando método de aplicación `configMode()`.

El modo de la aplicacion es declarado durante la instanciación, ya sea como una variable 
de ambiente o como un argumento en el constructor de la aplicación Slim. No puede ser 
cambiado posteriormente. El modo puede ser lo que quieras — "development", "test", y "production" 
son típicos, pero eres libre de usar el valor que quieras (por ejemplo "foo").

    <?php
    $app = new \Slim\Slim(array(
        'mode' => 'development'
    ));

Tipo de dato
: string

Valor por defecto
: "development"

### debug

<div class="alert alert-info">
    <strong>Importante!</strong> Slim convierte los errores en instancias de `ErrorException`
</div>

Si debugging esta habilitado, Slim va a usar su manejador de errores por defecto para 
mostrar información de diagnostico para las Excepciones no atrapadas. Si debugging esta 
deshabilitado, Slim va a invocar tu manejador de errores en su lugar, pasando la excepción 
sin atrapar como su primer y único argumento.

    <?php
    $app = new \Slim\Slim(array(
        'debug' => true
    ));

Tipo de dato
: boolean

Valor por defecto
: true

### log.writer

Usa un escritor de registro personalizado para almacenar los mensajes de registro en su 
destino correcto. Por defecto, el logger de Slim va a escribir los mensajes en `STDERR`. 
Si usas un escritor de registro personalizado, debe implementar esta interface:

    public write(mixed $message, int $level);

El método `write()` es responsable de enviar el mensaje de registro (no necesariamente un string) al destino 
apropiado (por ejemplo un archivo de texto, base de datos o un servicio web remoto).

Para especificar un escritor de registro personalizado después de la instanciación 
debes acceder al logger de Slim directamente y usar su método `setWriter()`:

    <?php
    // Durante la instanciación
    $app = new \Slim\Slim(array(
        'log.writer' => new \My\LogWriter()
    ));

    // Después de la instanciación
    $log = $app->getLog();
    $log->setWriter(new \My\LogWriter());

Tipo de dato
: mixed

Valor por defecto
: \Slim\LogWriter

### log.level

<div class="alert alert-info">
    <strong>Importante!</strong> Usa las constantes definidas en `\Slim\Log` en lugar de integers.
</div>

Slim tiene los siguientes niveles de registro:

* \Slim\Log::EMERGENCY
* \Slim\Log::ALERT
* \Slim\Log::CRITICAL
* \Slim\Log::ERROR
* \Slim\Log::WARN
* \Slim\Log::NOTICE
* \Slim\Log::INFO
* \Slim\Log::DEBUG

La opción `log.level` determina que mensaje de registro sera tomado en cuenta y cual sera ignorado. 
Por ejemplo, si la opción `log.level` es `\Slim\Log::INFO`, los mensajes de debug serán ignorados mientras 
que los errores info, warn, error y fatal serán almacenados.

Para cambiar esta opción después de la instanciación debes acceder al logger de Slim 
directamente y usar su método `setLevel()`.

    <?php
    // Durante la instanciación
    $app = new \Slim\Slim(array(
        'log.level' => \Slim\Log::DEBUG
    ));

    // Después de la instanciación
    $log = $app->getLog();
    $log->setLevel(\Slim\Log::WARN);

Tipo de dato
: integer

Valor por defecto
: \Slim\Log::DEBUG

### log.enabled

Esto habilita o deshabilita el logger de Slim. Para cambiar esta opción después de la instanciación 
debes acceder al logger de Slim directamente y usar su método `setEnabled()`.

    <?php
    // Durante la instanciación
    $app = new \Slim\Slim(array(
        'log.enabled' => true
    ));

    // Después de la instanciación
    $log = $app->getLog();
    $log->setEnabled(true);

Tipo de dato
: boolean

Valor por defecto
: true

### templates.path

La ruta relativa o absoluta al directorio de sistema que contiene las plantillas de tu 
aplicación Slim. La ruta es referenciada por la clase View de la aplicación Slim para 
obtener y mostrar las plantillas.

Para cambiar esta opción después de la instanciación debes acceder al View de Slim y usar 
su método `setTemplatesDirectory()`.

    <?php
    // Durante la instanciación
    $app = new \Slim\Slim(array(
        'templates.path' => './templates'
    ));

    // Después de la instanciación
    $view = $app->view();
    $view->setTemplatesDirectory('./templates');

Tipo de dato
: string

Valor por defecto
: "./templates"

### view

La clase View o instancia usada por la aplicación Slim. Para cambiar esta opción después de la instanciación 
debes usar el método `view()` de la aplicación Slim.

    <?php
    // Durante la instanciación
    $app = new \Slim\Slim(array(
        'view' => new \My\View()
    ));

    // Después de la instanciación
    $app->view(new \My\View());

Tipo de dato
: string|\Slim\View

Valor por defecto
: \Slim\View

### cookies.encrypt

Determina si la aplicación Slim debe encriptar sus cookies HTTP.

    <?php
    $app = new \Slim\Slim(array(
        'cookies.encrypt' => true
    ));

Tipo de dato
: boolean

Valor por defecto
: false

### cookies.lifetime

Determina el tiempo de vida de las cookies HTTP creadas por la aplicación Slim. Si este es un integer, 
debe ser un timestamp UNIX valido en el cual la cookie va a expirar. Si es un string, sera analizado con 
la función `strtotime()` para extrapolar un timestamp UNIX valido en el cual la cookie va a expirar.

    <?php
    // Durante la instanciación
    $app = new \Slim\Slim(array(
        'cookies.lifetime' => '20 minutes'
    ));

    // Después de la instanciación
    $app->config('cookies.lifetime', '20 minutes');

Tipo de dato
: integer|string

Valor por defecto
: "20 minutes"

### cookies.path

Determina la ruta por defecto de las cookies HTTP si ninguno es especificado cuando se invocan 
los métodos `setCookie()` o `setEncryptedCookie()` de la aplicación Slim.

    <?php
    // Durante la instanciación
    $app = new \Slim\Slim(array(
        'cookies.path' => '/'
    ));

    // Después de la instanciación
    $app->config('cookies.path', '/');

Tipo de dato
: string

Valor por defecto
: "/"

### cookies.domain

Determina el dominio por defecto de las cookies HTTP si ninguno es especificado cuando se invocan 
los métodos `setCookie()` o `setEncryptedCookie()` de la aplicación Slim.

    <?php
    // Durante la instanciación
    $app = new \Slim\Slim(array(
        'cookies.domain' => 'domain.com'
    ));

    // Después de la instanciación
    $app->config('cookies.domain', 'domain.com');

Tipo de dato
: string

Valor por defecto
: null

### cookies.secure

Determina si las cookies seran enviadas solo via HTTPS. Puedes sobrescribir esta opción 
cuando se invocan los métodos `setCookie()` o `setEncryptedCookie()` de la aplicación Slim.

    <?php
    // Durante la instanciación
    $app = new \Slim\Slim(array(
        'cookies.secure' => false
    ));

    // Después de la instanciación
    $app->config('cookies.secure', false);

Tipo de dato
: boolean

Valor por defecto
: false

### cookies.httponly

Determina si las cookies seran enviadas solo via HTTP. Puedes sobrescribir esta opción 
cuando se invocan los métodos `setCookie()` o `setEncryptedCookie()` de la aplicación Slim.

    <?php
    // Durante la instanciación
    $app = new \Slim\Slim(array(
        'cookies.httponly' => false
    ));

    // Después de la instanciación
    $app->config('cookies.httponly', false);

Tipo de dato
: boolean

Valor por defecto
: false

### cookies.secret_key

La llave secreta usada para encriptar las cookies. Deberías cambiar esta opción si usas cookies HTTP 
encriptadas en tu aplicación Slim.

    <?php
    // Durante la instanciación
    $app = new \Slim\Slim(array(
        'cookies.secret_key' => 'secret'
    ));

    // Después de la instanciación
    $app->config('cookies.secret_key', 'secret');

Tipo de dato
: string

Valor por defecto
: "CHANGE_ME"

### cookies.cipher

El cifrador mcrypt usado por la encriptación de cookies HTTP. Ver [cifradores disponibles](http://php.net/manual/es/mcrypt.ciphers.php).

    <?php
    // Durante la instanciación
    $app = new \Slim\Slim(array(
        'cookies.cipher' => MCRYPT_RIJNDAEL_256
    ));

    // Después de la instanciación
    $app->config('cookies.cipher', MCRYPT_RIJNDAEL_256);

Tipo de dato
: integer

Valor por defecto
: MCRYPT_RIJNDAEL_256

### cookies.cipher_mode

El modo de cifradores mcrypt usado por la encriptación de cookies HTTP. Ver [modo de cifradores mcrypt](http://php.net/manual/es/mcrypt.ciphers.php).

    <?php
    // Durante la instanciación
    $app = new \Slim\Slim(array(
        'cookies.cipher_mode' => MCRYPT_MODE_CBC
    ));

    // Después de la instanciación
    $app->config('cookies.cipher_mode', MCRYPT_MODE_CBC);

Tipo de dato
: integer

Valor por defecto
: MCRYPT_MODE_CBC

### http.version

Por defecto, Slim regresa una respuesta HTTP/1.1 al cliente. Usa esta opción si necesitas regresar 
una respuesta HTTP/1.0. Esto es útil si usas PHPFog o una configuración de servidor nginx donde 
te comunicas con proxies en el backend en lugar de directamente con el cliente HTTP.

    <?php
    // Durante la instanciación
    $app = new \Slim\Slim(array(
        'http.version' => '1.1'
    ));

    // Después de la instanciación
    $app->config('http.version', '1.1');

Tipo de dato
: string

Valor por defecto
: "1.1"
