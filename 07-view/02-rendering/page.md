---
title: Renderizado
status: live
---

Puedes utilizar el método `render()` de tu aplicación Slim para solicitar al
objeto vista actual que renderice una plantilla con una colección determinada de 
variables. El método `render()` de la aplicación Slim hará `echo()` sobre la
salida generada por el objeto vista para que pueda ser capturada por un buffer 
de salida, y la añadirá automáticamente al cuerpo de respuesta del objeto respuesta.
No se asume nada sobre cómo se renderiza la plantilla; dicho proceso se delega en 
el objeto vista.

    <?php
    $app = new \Slim\Slim();
    $app->get('/books/:id', function ($id) use ($app) {
        $app->render('myTemplate.php', array('id' => $id));
    });

Si necesitas pasar datos desde el callback de la ruta al objeto vista, debes 
hacerlo de forma explícita pasando un array como segundo parámetro al método 
`render()` de la aplicación Slim, de esta forma:

    <?php
    $app->render(
        'myTemplate.php',
        array( 'name' => 'Josh' )
    );

También puedes fijar el código de status en la respuesta HTTP al mismo tiempo que 
renderizas una plantilla:

    <?php
    $app->render(
        'myTemplate.php',
        array( 'name' => 'Josh' ),
        404
    );
