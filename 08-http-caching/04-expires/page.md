---
title: Expires
status: live
---

Utilizado en conjunción con los métodos `etag()` o `lastModified()`, el 
método `expires()` fija una cabecera **Expires** en la respuesta HTTP, informando 
al cliente HTTP de cuando su caché-cliente para el contenido actual debe considerarse 
obsoleta. El cliente HTTP seguirá sirviendo el contenido desde su caché hasta 
que se alcance dicha fecha de caducidad, momento en el que dicho cliente HTTP 
enviará una petición GET condicional a la aplicación Slim.

El método `expires()` acepta un parámetro: un timestamp entero UNIX, o una cadena 
que pueda ser parseada con `strtotime()`.

    <?php
    $app->get('/foo', function () use ($app) {
        $app->etag('unique-resource-id');
        $app->expires('+1 week');
        echo "This will be cached client-side for one week";
    });
