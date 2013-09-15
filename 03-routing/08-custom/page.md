---
title: Métodos HTTP Personalizados
status: live
---

### Una ruta, múltiples métodos HTTP

Algunas veces puedes necesitar que na ruta responda a múltiples métodos HTTP; algunas veces 
puedes necesitar que una ruta responda a un métodos HTTP personalizado. Puedes lograr ambas 
con el método `via()` del objeto Route. Este ejemplo demuestra como enlazar un URI del 
recurso a una función que responde a múltiples métodos HTTP.

    <?php
    $app = new \Slim\Slim();
    $app->map('/foo/bar', function() {
        echo "I respond to multiple HTTP methods!";
    })->via('GET', 'POST');
    $app->run();

La ruta definida en este ejemplo responderá a requests GET y POST del recurso identificado 
como “/foo/bar”. Especifica cada método HTTP apropiado como argumentos string separados en 
el método `via()` del objeto Request. Como otros métodos del enrutador (por ejemplo 
`name()` y `conditions()`), el método `via()` es enlazable:

    <?php
    $app = new \Slim\Slim();
    $app->map('/foo/bar', function() {
        echo "Fancy, huh?";
    })->via('GET', 'POST')->name('foo');
    $app->run();

### Una ruta, métodos HTTP personalizados

El método `via()` del objeto Route no esta limitado a solo métodos GET, POST, PUT, DELETE y OPTIONS. 
Puedes también usar tus propios métodos HTTP personalizados (por ejemplo si estuvieras respondiendo 
a request HTTP WebDAV). Puedes definir una ruta que responda a un método HTTP personalizado “FOO” 
de esta manera:

    <?php
    $app = new \Slim\Slim();
    $app->map('/hello', function() {
        echo "Hello";
    })->via('FOO');
    $app->run();
