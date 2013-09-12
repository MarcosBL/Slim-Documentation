---
title: Response - Introducción
status: live
---

Cada instancia de aplicación Slim tiene un objeto response. El objeto response 
es una abstracción del objeto HTTP response de tu applicación Slim que es 
devuelta al cliente HTTP. Aunque cada aplicación Slim incluye un objeto de 
response por defecto, la clase `\Slim\Http\Response` es idempotente; puedes
instanciar la clase a tu gusto (en un middleware o en cualquier parte de tu 
aplicación Slim) sin afectar a la aplicación como conjunto. Puedes obtener
una referencia al objeto response de la aplicación Slim con:

    <?php
    $app = new \Slim\Slim();
    $app->response;

Un objeto response HTTP tiene tres propiedades primarias:

* Status
* Header
* Body

El objeto response provee métodos helper, descritos a continuación, que te 
ayudarán a interactuar con dichas propiedades del objeto response HTTP. El 
objeto por defecto devolverá un response HTTP **200 OK** con el content-type 
**text/html**
