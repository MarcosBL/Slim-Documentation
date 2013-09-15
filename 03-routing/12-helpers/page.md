---
title: Métodos de ayuda de Ruta
status: live
---

Slim proporciona varios métodos de ayuda (expuestos a través de la instancia de la aplicación Slim) que pueden 
ayudar a controlar el flujo de tu aplicación.

Por favor ten en cuenta que los métodos de ayuda `halt()`, `pass()`, `redirect()` y `stop()` de la instancia de la aplicación 
son implementados usando excepciones. Cada uno lanzara una excepcion `\Slim\Exception\Stop` o `\Slim\Exception\Pass`. 
Lanzar una excepción en estos casos es una manera simple de detener la ejecución del código del usuario, hacer que 
el framework se haga cargo e inmediatamente enviar la respuesta necesaria al cliente. Este comportamiento puede tomar 
por sorpresa si no es esperado. Echa un vistazo al siguiente código:

    <?php
    $app->get('/', function() use ($app, $obj) {
        try {
            $obj->thisMightThrowException();
            $app->redirect('/success');
        } catch(\Exception $e) {
            $app->flash('error', $e->getMessage());
            $app->redirect('/error');
        }
    });

Si `$obj->thisMightThrowException()` lanza una excepción el código correrá como se espera. Sin embargo, si una excepción 
no es lanzada la llamada a $app->redirect() lanzara una excepción `\Slim\Exception\Stop` que sera atrapada por el bloque 
`catch` en lugar de que el framework redireccione al navegador a la pagina "/error". Cuando sea posible en tu aplicación 
deberías usar excepciones especificas para que tus bloques `catch` sean mas mejor dirigidos en lugar de atrapar todas 
las excepciones. En algunos casos `thisMightThrowException()` puede ser una llamada a un componente externo que no puedes 
controlar, in esta caso escribir todas las excepciones lanzadas puede no ser factible. Para esta instancia podemos ajustar 
nuestro código un poco al mover la llamada `$app->redirect()` después del bloque try/catch para resolver el problema. 
Dado que de detendrá el proceso en el error de redireccionamiento el código se ejecutara como se espera.

    <?php
    $app->get('/', function() use ($app, $obj) {
        try {
            $obj->thisMightThrowException();
        } catch(Exception $e) {
            $app->flash('error', $e->getMessage());
            $app->redirect('/error');
        }
        $app->redirect('/success');
    });

### Interrumpir

El método `halt()` de la aplicación Slim devolverá inmediatamente una respuesta HTTP con un código de estatus y cuerpo dado. 
Este método acepta dos argumentos: El código de estatus HTTP y un mensaje opcional. Slim va a parar inmediatamente la aplicación 
actual y enviara una respuesta HTTP al cliente con el estatus especificado y el mensaje opcional (como el cuerpo de la respuesta). 
Esto va a sobrecargar el objeto `\Slim\Http\Response` existente.

    <?php
    $app = new \Slim\Slim();

    //Enviar una respuesta de error 500
    $app->halt(500);

    //O si encuentras un Balrog...
    $app->halt(403, 'You shall not pass!');

Si quieres mostrar una plantilla con una lista de mensajes de error, puedes usar el método `render()` de la aplicación Slim en su lugar.

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () use ($app) {
        $errorData = array('error' => 'Permission Denied');
        $app->render('errorTemplate.php', $errorData, 403);
    });
    $app->run();

El método `halt()` puede enviar cualquier tipo de respuesta HTTP al cliente: informacional, éxito, redirección, no encontrado, 
error de cliente o error de servidor.

### Pasar

Una ruta puede decirle a la aplicación Slim que continúe a la siguiente rute que coincida usando el método de 
aplicación Slim `pass()`. Cuando este método es invocado, la aplicación Slim inmediatamente dejara de procesar la 
ruta actual e invocara la próxima ruta que coincida. Si no se consigue una ruta, una respuesta **404 No Encontrado** es 
enviada al cliente. Aquí hay un ejemplo. Asumiendo un request HTTP a “GET /hello/Frank”.

    <?php
    $app = new \Slim\Slim();
    $app->get('/hello/Frank', function () use ($app) {
        echo "You won't see this...";
        $app->pass();
    });
    $app->get('/hello/:name', function ($name) use ($app) {
        echo "But you will see this!";
    });
    $app->run();

### Redireccionar

Es fácil redireccionar el cliente a oro URL con el método `redirect()` de la aplicación Slim. Este método acepta 
dos argumentos: el primero es el URL a donde el cliente sera redireccionado; el segundo argumento opcional es el 
código de estado HTTP. Por defecto el método `redirect()` enviara una respuesta **302 Redirección Temporal**.

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () use ($app) {
        $app->redirect('/bar');
    });
    $app->run();

O si deseas usar una redirección permanente, debes especificar el URL destino como primer parámetro y el código 
de estado HTTP como segundo parámetro.

    <?php
    $app = new \Slim\Slim();
    $app->get('/old', function () use ($app) {
        $app->redirect('/new', 301);
    });
    $app->run();

Este método automáticamente colocara la cabecera Location. La respuesta de redirección HTTP sera enviada al cliente 
HTTP inmediatamente.

### Parar

El método `stop()` de la aplicación Slim detendrá la aplicación Slim y enviará la respuesta HTTP actual al cliente tal 
cual. Sin importar mas nada. 

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () use ($app) {
        echo "You will see this...";
        $app->stop();
        echo "But not this";
    });
    $app->run();

### URL Para

El método `urlFor()` de la aplicación Slim te permite crear URLs dinámicamente para una ruta nombrada de esa manera, 
cuando el patrón de una ruta cambie, tus URLs se actualizaran automáticamente sin romper tu aplicación. Este ejemplo 
muestra como generar URLs para rutas nombradas:

    <?php
    $app = new \Slim\Slim();

    //Crear ruta nombrada
    $app->get('/hello/:name', function ($name) use ($app) {
        echo "Hello $name";
    })->name('hello');

    //Generar URL para la ruta nombrada
    $url = $app->urlFor('hello', array('name' => 'Josh'));

En este ejemplo, $url es “/hello/Josh”. Para usar el método `urlFor()`, debes asignar primero un nombre a una ruta. 
Luego, invocar el método `urlFor()`. El primer argumento es el nombre de la ruta, y el segundo argumento es un array 
asociativo usado para reemplazar los parámetros URL de la ruta con valores reales; las claves del array deben coincidir 
con los parámetros del URI de la ruta y los valores serán usados como sustitución.
