---
title: Hooks - Introducción
status: live
---

Una aplicación Slim facilita una serie de hooks a los que puedes asociar tus 
propios callbacks.

### ¿Qué es un hook?

Un “hook” es un momento del ciclo de vida de la aplicación Slim en que una lista 
prioritizada de “callable” asignadas al hook serán invocadas. Un hook se indentifica 
por un nombre en formato cadena de texto.

Un “callable” es algo que devuelve `true` para `is_callable()`. Un callable será 
asignado a un hook y se invocará cuando se llame a dicho hook. Si hay múltiples 
callables asignados a un solo hook, cada callable será invocado en el orden asignado.
