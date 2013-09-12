---
title: Response Body
status: live
---
La respuesta HTTP devuelta al cliente dispondrá de un cuerpo. El cuerpo HTTP es
el contenido actual de la respuesta HTTP enviada al cliente. Puedes utilizar el 
objeto response de la aplicación Slim para asignar el cuerpo de la respuesta HTTP:

    <?php
    $app = new \Slim\Slim();

    // Overwrite response body
    $app->response->setBody('Foo');

    // Append response body
    $app->response->write('Bar');

Cuando sobreescribes o añades al cuerpo del objeto respuesta, dicho objeto respuesta 
asignará automáticamente la cabecera **Content-Length** basándose en el tamaño en 
bytes del nuevo cuerpo de respuesta.

Puedes obtener el cuerpo del objeto respuesta de esta forma:

    <?php
    $body = $app->response->getBody();

Por lo general, nunca necesitarás asignar el cuerpo de la respuesta manualmente con 
los métodos `setBody()` o `write()` methods; en su lugar, la aplicación Slim
lo hará por ti. Cada vez que hagas un `echo()` de contenido dentro de la función
callback de una ruta, el contenido del `echo()` es capturado en un buffer de salida
y añadido al cuerpo de respuesta antes de que la respuesta HTTP sea enviada al 
cliente.