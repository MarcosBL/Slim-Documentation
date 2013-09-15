---
title: Hooks por defecto
status: live
---

Estos son los hooks que por defecto se invocan en una aplicación Slim.

slim.before
: Este hook se invoca antes de que la aplicación Slim se ejecute y antes de que 
el buffer de salida se active. Solo se activa una vez durante todo el ciclo de 
vida de la aplicación Slim.

slim.before.router
: Este hook se invoca tras activar el buffer de salida y antes de que el enrutado 
tenga lugar. Solo se activa una vez durante todo el ciclo de vida de la aplicación 
Slim.

slim.before.dispatch
: Este hook se invoca antes de que la ruta coincidente actual sea procesada. Por 
lo general este hook solo se activa una vez durante todo el ciclo de vida de la 
aplicación Slim; sin embargo, puede invocarse múltiples veces si una ruta 
coincidente decide pasar a la siguiente ruta coincidente.

slim.after.dispatch
: Este hook se invoca después de que la ruta coincidente haya sido procesada. Por 
lo general este hook solo se activa una vez durante todo el ciclo de vida de la 
aplicación Slim; sin embargo, puede invocarse múltiples veces si una ruta coincidente 
decide pasar a la siguiente ruta coincidente.

slim.after.router
: Este hook se invoca después de que la ruta coincidente haya sido procesada, antes 
de que la Respuesta haya sido enviada al cliente, y después de que el buffer de 
salida haya sido desactivado. Solo se activa una vez durante todo el ciclo de 
vida de la aplicación Slim.

slim.after
: Este hook se invoca después de que el buffer de salida haya sido desactivado y 
después de que la Respuesta haya sido enviada al cliente. Solo se activa una vez 
durante todo el ciclo de vida de la aplicación Slim.
