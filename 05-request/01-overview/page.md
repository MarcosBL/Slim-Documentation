---
title: Request - Introducción
status: live
---

Cada instancia de la aplicación Slim tiene un objecto request. El objecto request es una abstracción 
del request HTTP actual y permite interactuar fácilmente con las variables de ambiente de la aplicación 
Slim. Aunque cada aplicación Slim incluye un objeto request por defecto, la clase `\Slim\Http\Request` es 
idempotente; puedes instanciar la clase cuando quieras (en el middleware u otro lugar de tu aplicación Slim) 
sin afectar la aplicación como un todo. Puedes obtener una referencia del objeto request de la aplicación 
Slim de esta manera:

    <?php
    // Regresa una instancia de \Slim\Http\Request
    $request = $app->request;
