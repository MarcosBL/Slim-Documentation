---
title: Cuerpo del Request
status: live
---

Usa el método `getBody()` del objeto request para obtener el cuerpo puro del request HTTP enviado por el cliente 
HTTP. Esto es particularmente útil para aplicaciones Slim que consumen JSON o requests XML.

    <?php
    $app = new \Slim\Slim();
    $body = $app->request->getBody();
