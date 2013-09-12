---
title: Cabeceras de Respuesta
status: live
---
La respuesta HTTP devuelta al cliente HTTP dispondrá de una cabecera. La cabecera 
HTTP es una lista de claves y valores que proveen metadatos sobre la respuesta 
HTTP. Puedes utilizar el objeto respuesta de la aplicación Slim para asignar esta
cabecera HTTP de respuesta. El objeto respuesta tiene una propiedad pública 
`headers` que es una instancia de `\Slim\Helper\Set`; esto facilita una interfaz
simple y estandarizada para manipular cabeceras de respuesta HTTP.

    <?php
    $app = new \Slim\Slim();
    $app->response->headers->set('Content-Type', 'application/json');

También puedes recoger encabezados del objeto `headers` de la respuesta:

    <?php
    $contentType = $app->response->headers->get('Content-Type');

Si un encabezado con el nombre indicado no existe, se devolverá `null`. Puedes
especificar los nombres de las cabeceras con mayúsculas, minúsculas, o una 
combinación de ambos con guiones o guiones bajos. Utiliza la convención de 
nombres con la que te sientas más cómodo.
