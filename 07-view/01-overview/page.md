---
title: Vistas - Introducción
status: live
---

Una aplicación Slim delega el rendrrizado de plantillas a su objeto vista. 
La vista de la aplicación Slim es una subclase de `\Slim\View` que implementa
esta interfaz:

    <?php
    public render(string $template);

El método `render` del objeto vista devolverá el contenido renderizado de la 
plantilla especificada por su argumento `$template`.
 