---
title: Cómo utilizar los Hooks
status: live
---

Se asigna un callable a un hook utilizando el método `hook()` de la aplicación 
Slim:

    <?php
    $app = new \Slim\Slim();
    $app->hook('the.hook.name', function () {
        //Hacer algo
    });

El primer parámetro es el nombre del hook, y el segundo parámetro es el callable. 
Cada hook mantiene una lista prioritizada de callables registrados. Por defecto, 
a cada callable asignado a un hook se le asigna una prioridad de 10. Puedes dar a 
tu callable una prioridad diferente pasando un entero como tercer parámetro al 
método `hook()`:

    <?php
    $app = new \Slim\Slim();
    $app->hook('the.hook.name', function () {
        //Hacer algo
    }, 5);

En el ejemplo anterior, asignamos una prioridad de 5 a nuestro callable. Cuando 
se llame al hook, ordenará todos los callables que tenga asignados de forma acorde 
a su prioridad (ascendente). Un callable con prioridad 1 será invocado antes que 
un callable con prioridad 10.

Los Hooks no pasan parámetros a sus callables. Si un callable necesita acceder a 
la aplicación Slim, puedes inyectar la aplicación en el callback con la palabra 
clave `use` o con el método estático de la aplicación Slim `getInstance()`:

    <?php
    $app = new \Slim\Slim();
    $app->hook('the.hook.name', function () use ($app) {
        // Hacer algo
    });
