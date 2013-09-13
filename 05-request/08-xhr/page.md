---
title: XMLHttpRequest
status: live
---

Cuando se use un framework de Javascript como MooTools o jQuery para ejecutar un XMLHttpRequest, el XMLHttpRequest 
sera enviado usualmente con una cabecera de HTTP **X-Requested-With**. La aplicacion Slim detectara la cabecera 
**X-Requested-With** del request HTTP y marcara el request como tal. Si por alguna razon un XMLHttpRequest no 
puede ser enviada con la cabecera de HTTP **X-Requested-With**, puedes forzar a la aplicacion Slim a asumir que 
un request es XMLHttpRequest al colocar un parametro GET, POST o PUT en el request HTTP llamado “isajax” con un 
valor verdadero.

Puedes usar los metodos `isAjax()` o `isXhr()` del objeto request para saber si el request actual es un request XHR/Ajax:

    <?php
    $isXHR = $app->request->isAjax();
    $isXHR = $app->request->isXhr();
