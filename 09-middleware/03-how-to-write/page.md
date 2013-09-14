---
title: Cómo escribir Middleware
status: live
---

El middleware de una aplicación Slim debe instanciarse como subclase de 
`\Slim\Middleware` e implementar un método público `call()`. El método `call()` 
no acepta parámetros. El Middleware debería implementar su propio constructor, 
propiedades y métodos. Te recomiendo encarecidamente dar un vistazo al middleware 
ya incluído en Slim para ver ejemplos funcionales (p.e. Slim/Middleware/ContentTypes.php 
o Slim/Middleware/SessionCookie.php).

Este ejemplo es la implementación mínima de un middleware en una aplicación Slim. 
Extiende `\Slim\Middleware`, implementa un método público `call()`, y llama al 
siguiente middleware interno.

    <?php
    class MyMiddleware extends \Slim\Middleware
    {
        public function call()
        {
            $this->next->call();
        }
    }
