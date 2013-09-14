---
title: Middleware - Introducción
status: live
---

El Framework Slim implementa una versión del protocolo Rack. Por tanto, una 
aplicación Slim puede tener middleware que puede inspeccionar, analizar, o 
modificar el embiente de la aplicación, sus peticiones, y respuestas antes y/o 
después de que la aplicación Slim haya sido instanciada.

### Arquitectura del Middleware

Piensa en la aplicación Slim como el núcleo de una cebolla. Cada capa de la 
cebolla es un middleware. Cuando llamas al método `run()` de la aplicación Slim, 
la capa más externa de middleware se ejecuta en primer lugar. Cuando está lista, 
dicha capa de middleware es la responsable de llamar a la siguiente capa middleware 
a la que rodea. Este proceso profundiza cada vez más en la cebolla - a través de 
cada capa de middleware - hasta que se llega al núcleo de la aplicación Slim. Este 
proceso por pasos es posible gracias a que cada capa de middleware, y la propia 
aplicación Slim, implementan un método público `call()`.
Cuando añades nuevo middleware a una aplicación Slim, el middleware añadido se 
convierte en una nueva capa externa y rodea la capa externa previa (si hay alguna) 
o a la propia aplicación Slim.

### Referencia de la Aplicación

La finalidad del middleware es inspeccionar, analizar, o modificar el ambiente de 
la aplicación, sus peticiones, y respuesta antes y/o después de la llamada a la 
aplicación Slim. Para cada middleware es sencillo el obtener referencias a la aplicación 
Slim primaria para descubrir su ambiente, peticiones, y respuesta:

    <?php
    class MyMiddleware extends \Slim\Middleware
    {
        public function call()
        {
            //La aplicación Slim
            $app = $this->app;

            //El objeto Ambiente
            $env = $app->environment;

            //El objeto Petición
            $req = $app->request;

            //El objeto Respuesta
            $res = $app->response;
        }
    }

Los cambios realizados a los objetos ambiente, peticiones y respuesta se propagarán 
inmediatamente a través de la aplicación y sus capas de middleware. Esto es posible 
porque cada capa de middleware recibe una referencia al mismo objeto de aplicación 
Slim.

### Referencia al Siguiente Middleware

Cada capa de middleware dispone además de una referencia a la siguiente capa interna 
de middleware con `$this->next`. Es responsabilidad de cada middleware el invocar 
o no al siguiente middleware. De esta forma, permitimos a la aplicación Slim el 
completar su ciclo de vida. Si una capa de middleware decide **no** invocar a la 
siguiente capa, el siguiente middleware interno y la propia aplicación Slim no se 
ejecutarán, y la respuesta actual de la aplicación se enviará al cliente HTTP tal 
cual esté.

    <?php
    class MyMiddleware extends \Slim\Middleware
    {
        public function call()
        {
            //Es opcional el invocar al siguiente middleware
            $this->next->call();
        }
    }
