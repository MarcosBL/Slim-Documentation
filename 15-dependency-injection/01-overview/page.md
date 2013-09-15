---
title: Inyección de Dependencia - Introducción
status: live
---

Slim tiene un localizador de recursos integrado que provee una manera fácil de inyectar objetos 
en una aplicación Slim, o para sobrecargar cualquiera de los objetos internos de una aplicación 
Slim (por ejemplo Request, Response, Log).)

## Inyectar valores simples

Si quieres usar Slim simplemente como un almacenador de clave-valor, es tan simple como esto:

    <?php
    $app = new \Slim\Slim();
    $app->foo = 'bar';

Ahora puedes obtener este valor en cualquier lado con `$app->foo` y recibir su valor `bar`.

## Usando el localizador de recursos

También puedes usar Slim como un localizador de recursos inyectando funciones que definan como 
serán construidos tus objetos deseados. Cuando la función inyectada es solicitada, sera invocada 
y su valor devuelto sera regresado.

    <?php
    $app = new \Slim\Slim();

    // Determina metodo para crear UUIDs
    $app->uuid = function () {
        return exec('uuidgen');
    };

    // Obtener nuevo UUID
    $uuid = $app->uuid;

### Recursos singulares

Algunas veces, puedes necesitar que tus definiciones de recursos se mantengan iguales cada vez 
que son solicitadas (por ejemplo deben ser singulares dentro del alcance de la aplicación Slim). 
Esta es una manera fácil de hacerlo:

    <?php
    $app = new \Slim\Slim();

    // Definir recurso log
    $app->container->singleton('log', function () {
        return new \My\Custom\Log();
    });

    // Obtener recurso log
    $log = $app->log;

Cada vez que solicites el recurso log con `$app->log`, este regresara la misma instancia.

### Recursos de cierre

¿Que si quieres almacenar literalmente una función como valor puro y no hacer que sea invocada? Puedes 
hacerlo de esta manera:

    <?php
    $app = new \Slim\Slim();

    // Definir función
    $app->myClosure = $app->container->protect(function () {});

    // Regresa función pura sin invocarla
    $myClosure = $app->myClosure;
