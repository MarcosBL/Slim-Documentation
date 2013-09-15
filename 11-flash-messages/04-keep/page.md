---
title: Flash Mantenidos
status: live
---

Este método le dice a la aplicación Slim que debe mantener los mensajes Flash 
existentes, fijados en la petición anterior, de forma que sigan estando disponibles 
en la siguiente petición. Este método es útil para persistir mensajes Flash tras 
hacer redirecciones HTTP.

    <?php
    $app->flashKeep();
