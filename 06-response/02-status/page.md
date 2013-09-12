---
title: Status de Respuesta
status: live
---

El objeto de respuesta HTTP devuelto al cliente dispondrá de un código de status
indicando el tipo de respuesta (p.e. 200 OK, 400 Bad Request, o 500 Server Error).
Puedes utilizar el objeto response de la aplicación Slim para fijar el estado de
la respuesta HTTP de esta forma:

    <?php
    $app->response->setStatus(400);

Solo necesitas asignar el estado del objeto response si deseas generar una
respuesta HTTP *que no* tenga un status 200 OK. También puedes obtener el estado 
actual del status HTTP de respuesta invocando al mismo método sin argumentos, de
esta forma:

    <?php
    $status = $app->response->getStatus();
