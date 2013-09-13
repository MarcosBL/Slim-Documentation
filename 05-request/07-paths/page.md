---
title: Rutas de Request
status: live
---

Cada request HTTP recibida por una aplicación Slim tendrá un URI raíz y un URI de recursos.

### URI raíz

La **URI raíz** es la ruta URL física del directorio en el que la aplicación Slim es instanciada y corrida. 
Si una aplicación Slim es instanciada en **index.php** dentro del directorio base de la raíz de documento 
en una maquina virtual, el URI raíz sera un string vacío. Si una aplicación Slim es instanciada y corrida en 
**index.php** dentro de un subdirectorio físico de la raíz de documento de una maquina virtual, el URI raíz sera 
la ruta a ese subdirectorio con una barra oblicua al principio y sin una barra oblicua al final.

### URI del Recurso

El **URI del recurso** es la ruta virtual URI de un recurso de la aplicación. El URI del recurso sera comparado 
con las rutas de la aplicación Slim.

Asumiendo que la aplicación Slim esta instalada en un subdirectorio físico **/foo** debajo de la raíz de documento 
de tu host virtual. También asumiendo que el request URL completo (lo que verías en el navegador en la barra de direcciones) 
es **/foo/books/1**. La URI raiz es **/foo** (la ruta al directorio físico donde la aplicación Slim es instanciada) y el URI 
del recurso es **/books/1** (la ruta al recurso de la aplicación).

Puedes obtener la URI raíz y URI del recurso del request HTTP con los métodos `getRootUri()` y `getResourceUri()` 
del objeto request:

    <?php
    $app = new \Slim\Slim();

    // Obtener objeto request
    $req = $app->request;

    // Obtener URI raíz
    $rootUri = $req->getRootUri();

    // Obtener URI del recurso
    $resourceUri = $req->getResourceUri();
