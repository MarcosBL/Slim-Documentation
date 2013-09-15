---
title: Escritores de Log
status: live
---

El objeto log de la aplicación Slim dispone de un escritor de logs. El escritor 
de logs es el responsable de enviar un mensaje logueado a la salida apropiada 
(p.e. STDERR, un fichero de log, un servicio remoto, Twitter, o una base de datos). 
Por defecto, el objeto log de una aplicación Slim dispone de un escritor de log 
con la clase `\Slim\LogFileWriter`; este escritor de logs redirige la salida 
al gestor de recurso referenciado por la clave de ambiente de la aplicación 
**slim.errors** (por defecto, es “php://stderr”). También puedes definir y 
utilizar un escritor de logs a medida.

### ¿Cómo utilizar un escritor de logs a medida?

Un escritor de logs a medida debe implementar esta interfaz pública:

    <?php
    public function write(mixed $message);

Debes indicar al objeto log de la aplicación Slim que utilice tu escritor de logs 
a medida. Puedes hacerlo en la configuración de la aplicación al instanciarla, de 
esta forma:

    <?php
    $app = new \Slim\Slim(array(
        'log.writer' => new MyLogWriter()
    ));

También puedes definir un escritor de logs a medida con middleware así:

    <?php
    class CustomLogWriterMiddleware extends \Slim\Middleware
    {
        public function call()
        {
            //Fijamos el nuevo escritor de logs a medida
            $$this->app->log->setWriter(new \MyLogWriter());

            //Llamamos al próximo middleware
            $this->next->call();
        }
    }

Puedes definir un escritor de logs a medida de forma similar en un hook de aplicación 
o en el callback de una ruta así:

    <?php
    $app->hook('slim.before', function () use ($app) {
        $app->log->setWriter(new \MyLogWriter());
    });

Si solo necesitas redirigir la salida de errores a otro gestor de recurso, utiliza 
el escritor de log por defecto de la aplicación Slim; éste ya escribe los mensajes de log 
a un gestor de recurso. Solo necesitas asignar la variable de ambiente **slim.errors** 
a un gestor de recurso válido.
