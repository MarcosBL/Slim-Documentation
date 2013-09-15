---
title: Manejador de Errores
status: live
---

Puedes usar el método `error()` de la aplicación Slim para especificar un manejador de errores 
personalizado para ser invocado cuando un error o excepción ocurre. Los manejadores de errores 
personalizados solo son invocados si el depuramiento de la aplicación esta deshabilitado.

Un manejador de errores personalizado debería mostrar un mensaje amigable para usuarios que mitigue 
confusiones. Similar al método `notFound()` de la aplicación Slim, el método `error()` actúa tanto como 
getter como setter.

### Establecer el manejador de errores personalizado

Puedes establecer un manejador de errores personalizado pasando una función al método `error()` de la aplicación 
Slim como su primer y único argumento.

    <?php
    $app = new \Slim\Slim();
    $app->error(function (\Exception $e) use ($app) {
        $app->render('error.php');
    });

En este ejemplo, el manejador de errores personalizado acepta la excepción atrapada como su argumento. Esto 
te permite responder apropiadamente a diferentes excepciones. 

### Invocar el manejador de errores personalizado

Por lo general, la aplicación Slim invocara automáticamente al manejador de errores cuando una 
excepción o error ocurre. Sin embargo, también puedes invocar al manejador de errores manualmente con 
el método `error()` de la aplicación Slim (sin argumentos).
