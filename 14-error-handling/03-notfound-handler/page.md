---
title: Manejador No Encontrado
status: live
---

Es inevitable que alguien solicite una pagina que no exista. La aplicación Slim te permite definir 
fácilmente un manejador No Encontrado personalizado con el método `notFound()` de la aplicación Slim. El 
manejador No Encontrado sera invocado cuando no se encuentre una ruta que coincida con el request HTTP 
actual. Este método actúa tanto como getter como setter.

### Establecer el manejador No Encontrado

Si invocas el método `notFound()` de la aplicación Slim y especificas una función ejecutable como su primer 
y único argumento, este método registrara la función como el manejador No Encontrado. Sin embargo, el manejador 
registrado no sera invocado.

    <?php
    $app = new \Slim\Slim();
    $app->notFound(function () use ($app) {
        $app->render('404.html');
    });

### Invocar manejador No Encontrado

Si invocas al método `notFound()` de la aplicación Slim sin argumentos, este método invocara el manejador 
No Encontrado previamente registrado.

    <?php
    $app = new \Slim\Slim();
    $app->get('/hello/:name', function ($name) use ($app) {
        if ( $name === 'Waldo' ) {
            $app->notFound();
        } else {
            echo "Hello, $name";
        }
    });
