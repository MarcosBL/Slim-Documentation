---
title: Almacenamiento nativo de Sesión
status: live
---

Una aplicación Slim no da nada por hecho acerca de las sesiones. Si prefieres utilizar 
una sesión PHP, debes configurar e iniciar una sesión nativa de PHP con 
`session_start()` antes de instanciar la aplicación Slim.

Deberías también deshabilitar el limite de caché de sesión de PHP para que PHP 
no envíe cabeceras de caducidad de caché en la respuesta HTTP. Puedes deshabilitar 
el límite de caché de sesión de PHP con:

    <?php
    session_cache_limiter(false);
    session_start();
