---
title: Nombres y Alcances de la Aplicación
status: live
---

Cuando creas una aplicación Slim deberás usar varios alcances en tu código (por ejemplo alcance global y alcance de función). 
Probablemente necesites una referencia a tu aplicación Slim en cada alcance. Existen varias maneras de hacer esto:

* Usa nombres de aplicación con el método estático `getInstance()` de la aplicación Slim
* Pasa una instancia de la aplicación al alcance de función con la palabra clave `use` (Currying)

### Nombres de Aplicación

Cada aplicación Slim puede tener un nombre determinado. **Esto es opcional**. Los nombres te ayudan 
a obtener una referencia a una instancia de la aplicación Slim en cualquier alcance dentro de tu código. 
Así es como puedes colocar y obtener un nombre de aplicación:

    <?php
    $app = new \Slim\Slim();
    $app->setName('foo');
    $name = $app->getName(); // "foo"

### Resolución de Alcance

Así que, ¿cómo obtienes una referencia a tu aplicación Slim? El ejemplo de abajo demuestra como obtener una referencia 
a una aplicación Slim dentro de una función de callback de una ruta. La variable `$app` es usada en el alcance global para 
definir la ruta HTTP GET. Pero la variable `$app` también se necesita dentro del alcance del callback para mostrar una plantilla.

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () {
        $app->render('foo.php'); // <-- ERROR
    });

Este ejemplo falla porque la variable `$app` no esta disponible dentro de la función callback de la ruta.

#### Currying

Podemos inyectar la variable `$app` en la función de callback usando la palabra clave `use`:

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () use ($app) {
        $app->render('foo.php'); // <-- EXITO
    });

#### Obtener por el Nombre

También puedes usar el método estático `getInstance()` de la aplicación Slim:

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', 'foo');
    function foo() {
        $app = Slim::getInstance();
        $app->render('foo.php');
    }
