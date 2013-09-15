---
title: Rutas OPTIONS
status: live
---

Usa el método `options()` de la aplicación Slim para enlazar una función a una URL de recurso 
que es solicitada con el método HTTP OPTIONS.

    <?php
    $app = new \Slim\Slim();
    $app->options('/books/:id', function ($id) {
        //Regresa las cabeceras de la respuesta
    });

En este ejemplo, un request HTTP OPTIONS a “/books/1” invocará la función asociada, pasando “1” como 
argumento.

El primer argumento del método `options()` de la aplicación Slim es el URI del recurso. El ultimo argumento es 
cualquier cosa que regrese `true` para `is_callable()`. Usualmente, el ultimo argumento sera una 
[función anónima][anon-func].

### Sobrecarga del Método

Desafortunadamente, los navegadores modernos no proveen soporte nativo para requests HTTP OPTIONS. Para 
solucionar esta limitación, asegúrate que el método de tu formulario HTML es “post”, y luego agrega 
un parámetro para sobrecargar el método en tu formulario HTML de esta forma:

    <form action="/books/1" method="post">
        ... otros campos del formulario aqui...
        <input type="hidden" name="_METHOD" value="OPTIONS"/>
        <input type="submit" value="Fetch Options For Book"/>
    </form>

Si estas usando [Backbone.js][backbone] o un cliente HTTP de linea de comando, también puedes sobrecargar 
el método HTTP usando la cabecera **X-HTTP-Method-Override**.

[anon-func]: http://php.net/manual/en/functions.anonymous.php
[backbone]: http://documentcloud.github.com/backbone/
