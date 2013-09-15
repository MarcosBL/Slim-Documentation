---
title: Depuramiento
status: live
---

Puedes habilitar el depuramiento durante la instanciación de la aplicación con esta opción:

    <?php
    $app = new \Slim\Slim(array(
        'debug' => true
    ));

También puedes habilitar el depuramiento después de la instanciación con el método de 
`config()` de la aplicación Slim:

    <?php
    $app = new \Slim\Slim();

    //Habilitar depuramiento (habilitado por defecto)
    $app->config('debug', true);

    //Deshabilitar depuramiento
    $app->config('debug', false);

Si el depuramiento esta habilitado y una excepción o error ocurre, una pantalla de diagnostico aparecerá con la 
descripción del error, el archivo afectado, el numero de la linea del archivo y un rastro de la pila de errores. 
Si el depuramiento esta desactivado, el manejador de errores personalizado sera invocado en su lugar.
