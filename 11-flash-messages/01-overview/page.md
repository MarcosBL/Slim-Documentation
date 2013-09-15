---
title: Mensajes Flash - Introducción
status: live
---

<div class="alert alert-info">
    <strong>¡Información!</strong> Los mensajes Flash requieren el uso de sesiones. 
	si no utilizas el middleware <code>\Slim\Middleware\SessionCookie</code>, deberás 
	iniciar una sesión nativa de PHP por ti mismo.
</div>

Slim soporta mensajería Flash tal como Rails y otros frameworks web mayores. La 
mensajería Flash te permite definir mensajes que persistirán hasta la siguiente 
petición HTTP, pero no más allá. Esto es útil para mostrar mensajes al usuario 
tras un determinado evento o error.

Como veremos más adelante, los métodos `flash()` y `flashNow()` de una aplicación 
Slim aceptan dos parámetros: una clave y un mensaje.
La clave puede ser cualquier cosa que quieras y define cómo se accederá al mensaje 
en las plantillas de vista. Por ejemplo, si invoco el método `flash('foo', 'El mensaje foo')` 
con esos parámetros, podré acceder a dicho mensaje en las plantillas de la siguiente 
petición con `flash['foo']`.

Los mensajes Flash se mantienen con el uso de sesiones; las sesiones son obligatorias 
para que dichos mensajes Flash puedan funcionar. Los mensajes Flash se almacenan 
en `$_SESSION['slim.flash']`.

