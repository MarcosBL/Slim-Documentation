---
title: Flash en la Siguiente
status: live
---

El método `flash()` de la aplicación Slim fija un mensaje que estará disponible 
en las plantillas de vista de la siguiente petición.
El mensaje de este ejemplo estará disponible en la variable de plantilla `flash['error']`.

    <?php
    $app->flash('error', 'El email del usuario es obligatorio');
