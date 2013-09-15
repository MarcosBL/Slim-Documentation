---
title: Variables de Request
status: live
---

Un request HTTP puede tener variables asociadas (no confundir con variables de rute). Las variables 
GET, POST o PUT enviadas con el request HTTP actual son expuestas a través del objeto request de 
la aplicación Slim.

Si quieres leer rápidamente una variable de request sin considerar su topo, puedes usar el método `params()` 
del objeto request:

    <?php
    $app = new \Slim\Slim();
    $paramValue = $app->request->params('paramName');

El método `params()` primero intentara buscar variables PUT, luego variables POST y después variables GET. 
Si no consigue variables regresara `null`. Si solo quieres buscar por un tipo especifico de variable, puedes usar 
uno de estos métodos en su lugar:

    <?php
    //Variable GET
    $paramValue = $app->request->get('paramName');

    //Variable POST
    $paramValue = $app->request->post('paramName');

    //Variable PUT
    $paramValue = $app->request->put('paramName');

Si una variable no existe, cada método de arriba va a devolver `null`. También puedes invocar cualquiera de estas 
funciones sin el argumento para obtener un array de todas las variables de un mismo tipo:

    <?php
    $allGetVars = $app->request->get();
    $allPostVars = $app->request->post();
    $allPutVars = $app->request->put();
