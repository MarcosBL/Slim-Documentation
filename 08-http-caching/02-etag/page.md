---
title: ETag
status: live
---

Una aplicación Slim facilita soporte integrado para el cacheado utilizando Etags. 
Un Etag es un identificador único para una URL. Cuando se asigna una cabecera 
Etag con el método `etag()` de una aplicación Slim, el cliente HTTP enviará una 
cabecera **If-None-Match** con cada petición HTTP subsecuente de la misma URI. 
Si el valor Etag del recurso URI coincide con el encabezado **If-None-Match** de 
la petición HTTP, la aplicación Slim devolverá una respuesta HTTP 
**304 Not Modified** que indicará al cliente HTTP que debe seguir usando su 
caché; esto impide también a la aplicación Slim el servir todo el contenido de 
dicha URI, ahorrando ancho de banda y reduciendo el tiempo de respuesta.

Definir un Etag con Slim es muy simple. Llamaremos al método `etag()` de la 
aplicación Slim en el callback de nuestra ruta, pasándole un ID único como 
primer y único parámetro.

    <?php
    $app->get('/foo', function () use ($app) {
        $app->etag('unique-id');
        echo "This will be cached after the initial request!";
    });

Y eso es todo. Asegúrate de que el ID del Etag es único para el contenido indicado. 
Además, asegúrate de que el ID ETag cambia si el contenido cambia; si no, el cliente 
HTTP seguirá sirviendo su caché obsoleta.
