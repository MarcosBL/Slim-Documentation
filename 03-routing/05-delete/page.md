---
title: Rutas DELETE
status: live
---

Usa el método `delete()` de la aplicación Slim para enlazar una función a una URL de recurso 
que es solicitada con el método HTTP DELETE.

    <?php
    $app = new \Slim\Slim();
    $app->delete('/books/:id', function ($id) {
        //Eliminar libro identificado con by $id
    });

En este ejemplo, un request HTTP DELETE a “/books/1” invocará la función asociada, pasando “1” como 
argumento.

El primer argumento del método `delete()` de la aplicación Slim es el URI del recurso. El ultimo argumento es 
cualquier cosa que regrese `true` para `is_callable()`. Típicamente, el ultimo argumento sera una 
[función anónima][anon-func].

### Sobrecarga del Método

Desafortunadamente, los navegadores modernos no proveen soporte nativo para requests HTTP DELETE. Para 
solucionar esta limitación, asegúrate que el método de tu formulario HTML es “post”, y luego agrega 
un parámetro para sobrecargar el método en tu formulario HTML de esta forma:

    <form action="/books/1" method="post">
        ... otros campos del formulario aqui...
        <input type="hidden" name="_METHOD" value="DELETE"/>
        <input type="submit" value="Delete Book"/>
    </form>

Si estas usando [Backbone.js][backbone] o un cliente HTTP de linea de comando, también puedes sobrecargar 
el método HTTP usando la cabecera **X-HTTP-Method-Override**.

[anon-func]: http://php.net/manual/es/functions.anonymous.php
[backbone]: http://documentcloud.github.com/backbone/
