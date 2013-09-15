---
title: Rutas PATCH
status: live
---

Usa el método `patch()` de la aplicación Slim para enlazar una función a una URL de recurso 
que es solicitada con el método HTTP PATCH.

    <?php
    $app = new \Slim\Slim();
    $app->patch('/books/:id', function ($id) {
        // Parchar libro con un ID especifico
    });

En este ejemplo, un request HTTP DELETE a “/books/1” invocará la función asociada, pasando “1” como 
argumento.

El primer argumento del método `patch()` de la aplicación Slim es el URI del recurso. El ultimo argumento es 
cualquier cosa que regrese `true` para `is_callable()`. Usualmente, el ultimo argumento sera una 
[función anónima][anon-func].

[anon-func]: http://php.net/manual/es/functions.anonymous.php
