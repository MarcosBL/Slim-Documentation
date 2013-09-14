---
title: Rutas GET
status: live
---

Usa el método `get()` de la aplicación Slim para enlazar una función a una URL de recurso 
que es solicitada con el método HTTP GET.

    <?php
    $app = new \Slim\Slim();
    $app->get('/books/:id', function ($id) {
        //Mostrar libro identificado por $id
    });

En este ejemplo, un request HTTP GET a “/books/1” invocará la función asociada, pasando “1” como 
argumento.

El primer argumento del método `get()` de la aplicación Slim es el URI del recurso. El ultimo argumento es 
cualquier cosa que regrese `true` para `is_callable()`. Típicamente, el ultimo argumento sera una 
[función anónima][anon-func].

[anon-func]: http://php.net/manual/es/functions.anonymous.php
