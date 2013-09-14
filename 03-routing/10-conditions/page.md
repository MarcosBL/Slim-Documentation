---
title: Condiciones de Ruta
status: live
---

Slim te permite asignar condiciones a los parámetros de ruta. Si las condiciones especificas no se cumple, la ruta 
no correrá. Por ejemplo, si necesitas una ruta con un segundo argumento que debe ser un año valido de 4 dígitos, 
puede obligar esta condición de esta manera:

    <?php
    $app = new \Slim\Slim();
    $app->get('/archive/:year', function ($year) {
        echo "You are viewing archives from $year";
    })->conditions(array('year' => '(19|20)\d\d'));

Invoca el método `conditions()` del objeto Route. El primer y único argumento es un array asociativo con claves 
que concuerden alguno de los parámetros de la ruta y valores que sean expresiones regulares.

### Condiciones de Ruta en toda la Aplicación

Si varias de tus rutas en tu aplicación Slim aceptan el mismo parámetro y usan la misma condición, puedes definir 
condiciones por defecto en toda la aplicación de esta manera:

    <?php
    \Slim\Route::setDefaultConditions(array(
        'firstName' => '[a-zA-Z]{3,}'
    ));

Define condiciones de rota en toda la aplicación antes de definir las rutas de la aplicación. Cuando defines una 
ruta, la ruta automáticamente sera asignada a cualquier condición de ruta en toda la aplicación definida con 
`\Slim\Route::setDefaultConditions()`. Si por alguna razón necesitas obtener las condiciones de ruta de toda las 
aplicación, puedes hacerlo usando `\Slim\Route::getDefaultConditions()`. Este método estático regresa un array 
exactamente como fue definido en las condiciones de ruta por defecto.

Puedes sobrecargar una condición de ruta por defecto re-definiendo la condición de la ruta cuando defines la ruta, 
de esta manera:

    <?php
    $app = new \Slim\Slim();
    $app->get('/hello/:firstName', $callable)
        ->conditions(array('firstName' => '[a-z]{10,}'));

Puedes agregar condiciones nuevas a una ruta de esta manera:

    <?php
    $app = new \Slim\Slim();
    $app->get('/hello/:firstName/:lastName', $callable)
        ->conditions(array('lastName' => '[a-z]{10,}'));
