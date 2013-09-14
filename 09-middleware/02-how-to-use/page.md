---
title: Cómo utilizar Middleware
status: live
---

Utiliza el método `add()` de la instancia de la aplicación Slim para añadir nuevo 
middleware a una aplicación Slim. El nuevo middleware rodeará al añadido previamente, 
o a la propia aplicación Slim si no se ha añadido middleware previamente.

### Ejemplo de Middleware

Este middleware de ejemplo convertirá a mayúsculas todo el cuerpo de la respuesta 
HTTP de la aplicación Slim.

    <?php
    class AllCapsMiddleware extends \Slim\Middleware
    {
        public function call()
        {
            // Obtenemos una referencia a la aplicación
            $app = $this->app;

            // Ejecutamos el middleware interno y la aplicación
            $this->next->call();

            // Convertimos a mayúsculas el cuerpo de la respuesta
            $res = $app->response;
            $body = $res->getBody();
            $res->setBody(strtoupper($body));
        }
    }

### Añadir Middleware

    <?php
    $app = new \Slim\Slim();
    $app->add(new \AllCapsMiddleware());
    $app->get('/foo', function () use ($app) {
        echo "Hello";
    });
    $app->run();

El método `add()` de la aplicación Slim acepta un parámetro: una instancia 
middleware. Si dicha instancia requiere alguna configuración especial, debería 
implementarla en su propio constructor, de forma que pueda ser configurada antes 
de ser añadida a la aplicación Slim.

Cuando se ejecute la aplicación Slim de ejemplo anterior, el cuerpo de la 
respuesta HTTP será un entusiasta "HELLO";
