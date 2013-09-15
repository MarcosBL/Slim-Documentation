---
title: Cookies de Request
status: live
---

### Obtener Cookies

Una aplicación Slim va a leer automáticamente las cookies enviadas el el request HTTP actual. Puedes obtener 
los valores de una cookie con el método de ayuda `getCookie()` de la aplicación Slim de esta manera:

    <?php
    $app = new \Slim\Slim();
    $foo = $app->getCookie('foo');

Solo las cookies enviadas el el request HTTP actual son accesibles con este método. Si colocas una cookie durante 
el request actual, no sera accesible con este método sino hasta el proximo request. Ten en cuenta que el método 
`getCookie()` del objeto `\Slim\Slim` es una conveniencia. También puedes obtener el conjunto complete de cookies 
del request HTTP directamente del objeto \Slim\Http\Request de esta manera:

    <?php
    $cookies = $app->request->cookies;

Este devolverá una instancia de \Slim\Helper\Set así que puedes usar su interfaz simple y estandarizada para 
inspeccionar las cookies del request.

### Encriptación de Cookie

Opcionalmente puedes elegir encriptar todas las cookies almacenadas en el cliente HTTP con la opcion `cookies.encrypt` 
de la aplicacion Slim. Cuando esta opcion es `true`, todas las cookies sera encriptadas usando tu clave y cifrador designados.

Es realmente así de fácil. Las cookies sera encriptadas automáticamente antes de ser enviadas al cliente. También serán 
decriptadas en demanda cuando las obtienes con `\Slim\Slim::getCookie()` durante las siguientes requests.
