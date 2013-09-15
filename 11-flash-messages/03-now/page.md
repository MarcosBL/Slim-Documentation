---
title: Flash Ahora
status: live
---

El método `flashNow()` de la aplicación Slim fija un mensaje que estará disponible 
en las plantillas de vista de la petición actual. Los mensajes fijados con el método 
de instancia de la aplicación `flashNow()` no estarán disponibles en la siguiente 
petición. El mensaje de este ejemplo estará disponible en la variable de plantilla 
`flash['info']`.

    <?php
    $app->flashNow('info', 'Tu tarjeta de crédito ha caducado');
