---
title: Last Modified
status: live
---

Una aplicación Slim facilita soporte integrado para el cacheado utilizando la fecha 
de última modificación del contenido.  Si especificamos una fecha de última 
modificación, Slim informa al cliente HTTP de dicha fecha y hora en que el contenido 
actual fue modificado. El cliente HTTP envía entonces una cabecera **If-Modified-Since** 
con cada petición HTTP subsecuente de la misma URI. 
Si la fecha de última modificación que indicas coincide con el encabezado 
**If-Modified-Since** de la petición HTTP, la aplicación Slim devolverá una respuesta HTTP 
**304 Not Modified** que indicará al cliente HTTP que debe seguir usando su 
caché; esto impide también a la aplicación Slim el servir todo el contenido de 
dicha URI, ahorrando ancho de banda y reduciendo el tiempo de respuesta.

Definir una fecha de última modificación con Slim es muy simple. Llamaremos al 
método `lastModified()` de la aplicación Slim en el callback de nuestra ruta, 
pasándole un timestamp UNIX de la fecha de última modificación de nuestro 
contenido concreto. 

Asegúrate de que el timestamp del método `lastModified()` se actualiza al mismo 
tiempo que la fecha de moficiación del contenido; si no, el navegador cliente 
HTTP seguirá sirviendo su caché obsoleta.

    <?php
    $app->get('/foo', function () use ($app) {
        $app->lastModified(1286139652);
        echo "This will be cached after the initial request!";
    });
