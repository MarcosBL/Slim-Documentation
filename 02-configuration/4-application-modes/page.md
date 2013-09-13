---
title: Modos de la Aplicación
status: live
---

Es una practica común correr las aplicaciones web en diferentes modos dependiendo del estado actual del proyecto. 
Si estas desarrollando una aplicación, puedes correrla en modo “development”; si estas probando la aplicación, puedes 
correrla en modo “test”; si lanzas la aplicación, puedes correrla en modo “production”.

Slim suporta el concepto de modos de manera que puedes definir tus propios modos y permitir que Slim se 
prepare apropiadamente para el modo actual. Por ejemplo, tal vez quieras habilitar debugging en modo “development” pero 
no en modo “production”. El ejemplo de abajo demuestra como configurar Slim dependiendo del modo determinado.

### ¿Que es un modo?

Técnicamente, un modo de aplicación es simplemente una cadena de texto - como “development” o “production” - que tiene 
una función de callback asociada para preparar a la aplicación Slim apropiadamente. El modo de la aplicación puede ser 
lo que quieras: “testing”, “production”, “development”, o incluso “foo”.

### ¿Como coloco el modo de la aplicación?

<div class="alert alert-info">
    <strong>Importante!</strong> El modo de la aplicación solo puede ser colocado durante la instanciación de la aplicación. No puede ser cambiado luego.
</div>

#### Usar una variable de ambiente

Si Slim ve una variable de ambiente llamada "SLIM_MODE", colocara el modo de la aplicación al valor de esa variable.

    <?php
    $_ENV['SLIM_MODE'] = 'production';

#### Usar opciones de la aplicación

Si una variable de ambiente no es encontrada, Slim buscará el modo en las opciones de la aplicación.

    <?php
    $app = new \Slim\Slim(array(
        'mode' => 'production'
    ));

#### Modo por defecto

Si la variable de ambiente y la opción de configuración no son encontradas, Slim colocará el modo de la aplicación en “development”.

### Configure for a Specific Mode

Después de crear una instancia una aplicación Slim, puedes configurar la aplicación para un modo especifico 
con el método de aplicación Slim `configureMode()`. Este método acepta dos argumentos: el nombre del modo objetivo 
y una función para ser llamada inmediatamente si el primer argumento concuerda con el modo de aplicación actual.

Asumiendo que el modo de aplicación actual es “production”. Solo la función asociada con el modo “production” sera 
invocada. La función asociada con el modo “development” sera ignorada hasta que el modo de la aplicación cambie a 
“development”.

    <?php
    // Colocar el modo actual
    $app = new \Slim\Slim(array(
        'mode' => 'production'
    ));

    // Solo invocado si el modo es "production"
    $app->configureMode('production', function () use ($app) {
        $app->config(array(
            'log.enable' => true,
            'debug' => false
        ));
    });

    // Solo invocado si el modo es  "development"
    $app->configureMode('development', function () use ($app) {
        $app->config(array(
            'log.enable' => false,
            'debug' => true
        ));
    });
