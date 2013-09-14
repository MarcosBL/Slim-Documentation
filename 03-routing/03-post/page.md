---
title: Rutas POST
status: live
---

Usa el método `post()` de la aplicación Slim para enlazar una función a una URL de recurso 
que es solicitada con el método HTTP POST.

    <?php
    $app = new \Slim\Slim();
    $app->post('/books', function () {
        //Crear libro
    });

En este ejemplo, un request HTTP POST a “/books” invocará la función asociada.

El primer argumento del método `post()` de la aplicación Slim es el URI del recurso. El ultimo argumento es 
cualquier cosa que regrese `true` para `is_callable()`. Típicamente, el ultimo argumento sera una 
[función anónima][anon-func].

[anon-func]: http://php.net/manual/es/functions.anonymous.php
