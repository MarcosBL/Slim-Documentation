---
title: Hola Mundo
status: live
---

Crea una nueva instancia de Slim:

    $app = new \Slim\Slim();

Define una ruta HTTP GET:

    $app->get('/hello/:name', function ($name) {
        echo "Hello, $name";
    });

Corre la aplicación Slim:

    $app->run();
