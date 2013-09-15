---
title: Niveles de Log
status: live
---

<div class="alert alert-info">
    <strong>¡Información!</strong> Utiliza las constantes de <code>\Slim\Log</code> 
	cuando fijes el nivel de log en lugar de utilizar números enteros.
</div>

El objeto log de la aplicación Slim respetará o ignorará los mensajes logueados 
dependiendo de su ajuste de nivel de log. Cuando llamas a los métodos del objeto 
log, estás ya asignando un nivel al mensaje logueado de forma inherente.

Los niveles de log disponibles son:

\Slim\Log::EMERGENCY
: Nivel 1

\Slim\Log::ALERT
: Nivel 2

\Slim\Log::CRITICAL
: Nivel 3

\Slim\Log::ERROR
: Nivel 4

\Slim\Log::WARN
: Nivel 5

\Slim\Log::NOTICE
: Nivel 6

\Slim\Log::INFO
: Nivel 7

\Slim\Log::DEBUG
: Nivel 8

Solo los mensajes que tengan un nivel inferior al del objeto log actual serán 
logueados. Por ejemplo, si el nivel del objeto log es `\Slim\Log::WARN` (5), el 
objeto log ignorará los mensajes `\Slim\Log::DEBUG` y `\Slim\Log::INFO` pero 
aceptará los mensajes `\Slim\Log::WARN`, `\Slim\Log::ERROR`, y `\Slim\Log::CRITICAL`.

### ¿Cómo ajustar el nivel de log?

    <?php
    $app->log->setLevel(\Slim\Log::WARN);

También puedes ajustar el nivel del objeto log al instanciar la aplicación:

    <?php
    $app = new \Slim\Slim(array(
        'log.level' => \Slim\Log::WARN
    ));
