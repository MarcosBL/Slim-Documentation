---
title: Middleware de Ruta
status: live
---

Slim te permite asociar un middleware con una rute de aplicación especifica. Cuando la ruta dada coincide con 
el request HTTP actual y es invocada, Slim invocara primero el middleware asociado en el orden en el que 
son definidos.

### ¿Que es un middleware de ruta?

Un middleware de ruta es cualquier cosa que regrese `true` para `is_callable`. Los middleware de ruta sera invocados 
in la secuencia en que fueron definidos antes que su ruta relacionada sea invocada.

### ¿Como agrego un middleware de ruta?

Cuando defines una nueva ruta de aplicación con los métodos `get()`, `post()`, `put()`, o `delete()` de la aplicación 
Slim debes definir un patrón de ruta y una función para ser invocada cuando la ruta coincide con el request HTTP.

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () {
        //Hacer algo
    });

En el ejemplo de arriba, el primer argumento es el patrón de la ruta. El ultimo argumento es una función a ser 
invocada cuando la ruta coincida con el request HTTP actual. El patrón de la ruta siempre debe ser el primer argumento. 
La función de la ruta siempre debe ser el ultimo argumento.

Puedes asignar el middleware a esta ruta pasando cada middleware en el interior de los argumentos o... (ahem) el medio... 
de los argumentos de esta manera:

    <?php
    function mw1() {
        echo "This is middleware!";
    }
    function mw2() {
        echo "This is middleware!";
    }
    $app = new \Slim\Slim();
    $app->get('/foo', 'mw1', 'mw2', function () {
        //Haces algo
    });

Cuando la ruta /foo es invocada, las funciones `mw1` y `mw2` serán invocadas en secuencia antes que la función de la 
ruta sea invocada.

Supón que quieres autenticar al usuario actual con un rol determinado para una ruta especifica. Puedes usar algo de 
magia en la función de esta manera:

    <?php
    $authenticateForRole = function ( $role = 'member' ) {
        return function () use ( $role ) {
            $user = User::fetchFromDatabaseSomehow();
            if ( $user->belongsToRole($role) === false ) {
                $app = \Slim\Slim::getInstance();
                $app->flash('error', 'Login required');
                $app->redirect('/login');
            }
        };
    };
    $app = new \Slim\Slim();
    $app->get('/foo', $authenticateForRole('admin'), function () {
        //Mostrar panel de control de administración
    });

### ¿Que argumentos se pasan en cada función de middleware?

Cada función de middleware es invocada con un argumento, el objeto `\Slim\Route` que 
coincida actualmente:

    <?php
    $aBitOfInfo = function (\Slim\Route $route) {
        echo "Current route is " . $route->getName();
    };

    $app->get('/foo', $aBitOfInfo, function () {
        echo "foo";
    });
