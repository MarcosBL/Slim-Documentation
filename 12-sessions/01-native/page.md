---
title: Almacenamiento Nativo de Sesiones
status: live
---

Una aplicación Slim no asume nada acerca de las sesiones. Si prefieres usar sesiones PHP, debes configurar 
y habilitar la sesión nativa de PHP con `session_start()` antes de instanciar la aplicación Slim.

Deberías deshabilitar el limitado de cache de sesión de PHP para que PHP no envíe cabeceras de expiración de
cache con hagan conflicto con la respuesta HTTP. Puedes deshabilitar el limitador de cache de sesiones de PHP con:

    <?php
    session_cache_limiter(false);
    session_start();