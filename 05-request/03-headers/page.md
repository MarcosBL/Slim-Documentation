---
title: Cabezeras de Request
status: live
---

Una aplicación Slim automáticamente leerá todas las cabeceras del request HTTP. Puedes acceder a las 
cabeceras del request usando la propiedad publica del objeto de request `headers`. La propiedad `headers` 
es una instancia de `\Slim\Helper\Set`, lo que significa que provee una interfaz simple y estandarizada 
para interactuar con las cabeceras del request HTTP.

    <?php
    $app = new \Slim\Slim();

    // Obtener las cabeceras del request como array asociativo
    $headers = $app->request->headers;

    // Obtener la cabecera ACCEPT_CHARSET
    $charset = $app->request->headers->get('ACCEPT_CHARSET');

La especificación HTTP especifica que los nombres de las cabeceras HTTP pueden ser en mayúsculas, minúsculas 
o una combinación de ambas. Slim es suficientemente inteligente para leer y devolver los valores de la cabecera 
ya sea que los solicites usando el nombre en mayúsculas, minúsculas o una combinaciones de las dos, ya sea con 
barras bajas o guiones. Así que puedes usar la convención de nomenclatura con la que estés mas cómodo.
