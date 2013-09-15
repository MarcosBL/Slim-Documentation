---
title: Hooks a medida
status: live
---

Se pueden crear e invocar hooks a medida en una aplicación Slim. Cuando se invoca 
un hook a medida con `applyHook()`, llamará a todos los callables asignados al 
mismo. Así es exactamente como funcionan los hooks por defecto de una aplicación 
Slim. En este ejemplo, aplicaré un hook a medida llamado “my.hook.name”. Se 
llamará automáticamente a todos los callables registrados previamente para este hook.

    <?php
    $app = new \Slim\Slim();
    $app->applyHook('my.hook.name');

Cuando ejecutes el código anterior, todos los callables que hayan sido asignados 
previamente al "my.hook.name" serán invocados en order de prioridad (ascendente).

Deberías registrar callables a un hook antes de aplicarlo. Piensa en ellos de esta 
forma: cuando invocas al método `applyHook()` de una aplicación Slim, estás 
indicándole a Slim que llame a todos los callables registrados para dicho hook.
