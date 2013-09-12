---
title: Configuración - Introducción
status: live
---

Existen dos manera de configurar la aplicación Slim. Primero durante la instanciación 
y segundo después de la instanciación. Todas las opciones pueden ser aplicadas al 
momento de la instanciación pasando un array asociativo al constructor de la clase 
Slim. Todas las opciones pueden ser obtenidas y modificadas luego de la instanciación, 
sin embargo algunas de ellas no pueden ser cambiadas simplemente usando el método 
de la instancia de la aplicación pero sera demostrado cuando sea necesario más 
abajo. Antes de mostrar las opciones disponibles, quiero explicar rápidamente como 
puedes definir e inspeccionar las opciones en tu aplicación Slim.

### Durante la instanciación

Para definir opciones durante la instanciación, pasa un array asociativo en el constructor 
de Slim.

    <?php
    $app = new Slim(array(
        'debug' => true
    ));

### Después de la instanciación

Para definir opciones después de la instanciación, la mayoría puede usar el método de la instancia 
de la configuración de la aplicación; el primer argumento es el nombre de la opción y el segundo 
es el valor de la opción.

    <?php
    $app->config('debug', false);

También puedes definir múltiples opciones al mismo tiempo usando un array asociativo:

    <?php
    $app->config(array(
        'debug' => true,
        'templates.path' => '../templates'
    ));

Para obtener el valor de una opción, puedes usar también el método de la instancia 
de la configuración de la aplicación; sin embargo, solo pasas un solo argumento - 
el nombre de la opción a inspeccionar. Si la opción que pides no existe, `null` es 
regresado.

    <?php
    $settingValue = $app->config('templates.path'); //returns "../templates"

No estas limitado a las opciones mostradas abajo; también puedes definir tus 
propias opciones.
