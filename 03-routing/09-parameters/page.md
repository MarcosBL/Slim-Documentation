---
title: Parámetros de Ruta
status: live
---

Puedes utilizar parametros en las URIs de recurso de las rutas. En este ejemplo, existen dos 
parametros en el URI de la ruta, “:one” y “:two”.

    <?php
    $app = new \Slim\Slim();
    $app->get('/books/:one/:two', function ($one, $two) {
        echo "The first parameter is " . $one;
        echo "The second parameter is " . $two;
    });

Para crear un parámetro URL, coloca “:” al principio del nombre del parámetro en el patrón del URI 
de la ruta. Cuando la ruta coincida con el request HTTP actual, los valores de cada parámetro son extraídos 
del request HTTP y pasados en orden a la función asociada.

### Comodines en parámetros de ruta

Puedes usar comodines en los parámetros de la ruta. Estos capturaran uno o varios segmentos del URI que 
correspondan al patrón del comodín de la ruta en un array. Un parámetro comodín este identificado con un 
sufijo “+”; de otra manera actúa igual que un parámetro normal de ruta mostrado arriba. Aquí esta un ejemplo:

    <?php
    $app = new \Slim\Slim();
    $app->get('/hello/:name+', function ($name) {
        // Hacer algo
    });

Cuando invocas esta aplicación ejemplo con el URI de recurso “/hello/Josh/T/Lockhart”, el argumento `$name` de 
la función de la ruta sera igual a `array('Josh', 'T', Lockhart')`.

### Parametros de ruta opcionales

<div class="alert alert-warning">
    <strong>Importante!</strong> Los segmentos de ruta opcionales son experimentales. Solo deberían ser usados 
    en la manera mostrada abajo.
</div>

Puedes usar también parámetro de ruta opcionales. Estos son ideales para usar en un archivo de un blog. Para 
declarar parámetros de ruta opcionales, especifica el patrón de la ruta así:

    <?php
    $app = new Slim();
    $app->get('/archive(/:year(/:month(/:day)))', function ($year = 2010, $month = 12, $day = 05) {
        echo sprintf('%s-%s-%s', $year, $month, $day);
    });

Cada segmento de ruta subsecuente es opcional. Esta ruta aceptara request HTTP para:

* /archive
* /archive/2010
* /archive/2010/12
* /archive/2010/12/05

Si un segmento de ruta opcional es omitido del request HTTP, los valores por defecto en los argumentos de la 
función serán usados en su lugar.

Actualmente, solo puedes usar segmentos de ruta opcionales en situaciones como en el ejemplo de arriba donde 
cada segmento de ruta subsecuente es opcional. Puedes encontrar esta característica inestable cuando es usada 
en escenarios diferentes al del ejemplo de arriba.
