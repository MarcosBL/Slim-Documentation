---
title: Redirección de Salida
status: live
---

El ambiente de la aplicación Slim siempre contendrá una clave **slim.errors** con un valor que 
sea un recurso escribible donde los registros y mensajes de error puedan ser guardados. El objeto log de la aplicación 
Slim escribirá los mensajes de error en **slim.errors** cuando una excepción sea atrapada o el objeto log 
sea invocado manualmente.

Si quieres redireccionar la salida de errores a un ligar diferente, puedes definir tu propio recurso 
escribible modificando la opción del ambiente de la aplicación Slim. Te recomiendo que uses un middleware 
para actualizar en ambiente:

    <?php
    class CustomErrorMiddleware extends \Slim\Middleware
    {
        public function call()
        {
            // Establecer la nueva salida de errores
            $env = $this->app->environment;
            $env['slim.errors'] = fopen('/path/to/output', 'w');

            // Llamar al proximo middleware
            $this->next->call();
        }
    }

Recuerda, **slim.errors** no necesita apuntar a un archivo; puede apuntar a cualquier recurso escribible 
valido.
