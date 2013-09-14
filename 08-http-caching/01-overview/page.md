---
title: Cacheado HTTP - Introducción
status: live
---
Una aplicación Slim ofrece soporte integrado para el almacenamiento en caché HTTP 
con sus métodos de ayuda `etag()`, `lastModified()` y `expires()`. Lo mejor es 
utilizar o bien `etag ()` o bien `lastModified ()` - en conjunción con `expires()` 
- para cada ruta; Nunca debemos utilizar `etag()` y `lastModified()` juntos en el 
mismo callback de una ruta.

Los métodos `etag()` y `lastModified()` deben ser invocados en el callback de la 
ruta antes que cualquier otro código; esto permite a Slim comprobar peticiones GET 
condicionales antes de procesar el código restante del callback de la ruta.

Tanto `etag()` como `lastModified()` indican al cliente HTTP que almacene el 
contenido de respuesta en la memoria caché del lado del cliente.
El método `expires()` indica al cliente HTTP cuando la memoria del lado del 
cliente debe ser considerada obsoleta.
