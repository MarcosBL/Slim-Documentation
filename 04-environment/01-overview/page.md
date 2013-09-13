---
title: Ambiente - Introducción
status: live
---

Slim Framework implementa una derivación del [protocolo Rack](http://rack.rubyforge.org/doc/SPEC.html). 
Cuando creas una instancia de la aplicación Slim, esta inmediatamente inspecciona la superglobal `$_SERVER` 
y deriva un grupo de variables de ambiente que dictan el comportamiento de la aplicación.

### ¿Que es el Ambiente?

El ambiente de una aplicación Slim es un array asociativo de opciones que son leídas una vez y pueden se 
accedidas por la aplicación Slim y su middleware. Eres libre de modificar las variables de ambiente durante 
el tiempo de vida de la aplicación; los cambios van a propagar inmediatamente a través de la aplicación.

Cuando creas una instancia de una aplicación Slim, las variables de ambiente son derivadas de la superglobal 
`$_SERVER`; no necesitas colocarlas manualmente. Sin embargo, eres libre de modificar o suplementar estas 
variables in el middleware de Slim.

Estas variables son fundamentales para determinas como la aplicación Slim va a correr: el URI de los recursos, 
el método HTTP, el cuerpo del request HTTP, los parámetros del query URL, mensajes de error, y mas. El middleware, 
descrito mas adelante, te da el poder de - entre otras cosas - manipular las variables de ambiente antes y/o después 
que la aplicación Slim comience a correr.

### Variables de Ambiente

El siguiente texto toma prestado con respeto la misma información disponible en <http://rack.rubyforge.org/doc/SPEC.html>. 
El array de ambiente debe incluir estas variables:

REQUEST_METHOD
: El método del request HTTP. Este es requerido y nunca puede ser un string vacío.

SCRIPT_NAME
: La porción inicial de la “ruta” del request URI que corresponde al directorio físico en donde la aplicación Slim 
esta instalada — para que la aplicación sepa su “localización” virtual. Este puede ser un string vacío si la aplicación 
esta instalada en el nivel superior del directorio publico de la raíz del documento. Este nunca terminara con una barra oblicua.

PATH_INFO
: La porción restante de la “ruta” del request URI que determina la localización “virtual” del objetivo del request HTTP dentro del 
contexto de la aplicación Slim. Este siempre empezara con una barra oblicua; puede o puede no terminar con una barra oblicua.

QUERY_STRING
: La parte del request HTTP del URI después, pero no incluyendo, el “?”. Este es requerido pero puede ser un string vacío.

SERVER_NAME
: Cuando es combinado con `SCRIPT_NAME` y `PATH_INFO`, este puede ser usado para crear un URL completamente calificado a un 
recurso de la aplicación. Sin embargo, si `HTTP_HOST` esta presente, debe ser utilizado en lugar de este. Este es requerido y nunca 
puede ser un string vacío.

SERVER_PORT
: Cuando es combinado con `SCRIPT_NAME` y `PATH_INFO`, este puede ser usado para crear un URL completamente calificado a un 
recurso de la aplicación. Este es requerido y nunca puede ser un string vacío.

HTTP_*
: Las variables que coinciden con las cabeceras del request HTTP enviadas por el cliente. La existencia de estas variables 
corresponde con aquellas enviadas en el request HTTP actual.

slim.url_scheme
: Será “http” o “https” dependiendo del URL del request HTTP.

slim.input
: Será un string representando el cuerpo puro del request HTTP. Si el cuerpo del request HTTP esta vacio (por ejemplo con un request GET), 
este será un string vacio.

slim.errors
: Debe ser siempre un recurso escribible; por defecto, este es un recurso de solo escritura manejado por `php://stderr`.

La aplicación Slim puede almacenar sus propios datos en el ambiente también. Las claves del array del ambiente 
deben contener por lo menos un punto, y deben tener un prefijo único (por ejemplo “prefix.foo”). El prefijo **slim.** esta 
reservado para ser usado por Slim y no debe ser usado en cualquier otro caso. El ambiente no debe contener las claves 
`HTTP_CONTENT_TYPE` o `HTTP_CONTENT_LENGTH` (usar las versiones sin HTTP_). Las claves CGI (nombradas sin un punto) deben 
tener valores de tipo String. Existen las siguientes restricciones:

* slim.url_scheme debe ser “http” o “https”.
* `slim.input` debe ser un string.
* Debe haber un recurso valido y escribible en `slim.errors`.
* El `REQUEST_METHOD` debe ser un token valido.
* El `SCRIPT_NAME`, si no esta vacío, debe empezar con "/"
* El `PATH_INFO`, si no esta vacío, debe empezar con "/"
* El `CONTENT_LENGTH`, si es usado, debe consistir solo de dígitos.
* Alguno de `SCRIPT_NAME` o `PATH_INFO` debe ser colocado. `PATH_INFO` debería ser "/" si `SCRIPT_NAME` esta vacío. 
`SCRIPT_NAME` nunca debe ser "/", sino ser un string vacío.
