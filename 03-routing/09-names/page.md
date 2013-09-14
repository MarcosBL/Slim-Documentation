---
title: Nombres de Ruta
status: live
---

Slim te permite asignar un nombre a una ruta. Nombrar una ruta te permite generar URLs dinámicos usando 
el método de ayuda `urlFor()`. Cuando usas el método `urlFor()` de la aplicación Slim para crear URLs, 
puedes cambiar los patrones de la ruta libremente sin romper tu aplicación. Este es un ejemplo de una 
ruta con nombre:

    <?php
    $app = new \Slim\Slim();
    $app->get('/hello/:name', function ($name) {
        echo "Hello, $name!";
    })->name('hello');

Ahora puedes generar URLs para esta ruta usando el método `urlFor()`, descrito mas adelante en esta documentación. 
El método `name()` de la ruta también es enlazable:

    <?php
    $app = new \Slim\Slim();
    $app->get('/hello/:name', function ($name) {
        echo "Hello, $name!";
    })->name('hello')->conditions(array('name' => '\w+'));
