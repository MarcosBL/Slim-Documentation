---
title: Manipulación de Errores - Introducción
status: live
---

Seamos realistas: a veces las cosas salen mal. Es importante interceptar errores y responder a ellos 
apropiadamente. Una aplicación Slim provee de métodos de ayuda para responder a errores y excepciones.

### Notas Importantes

* Una aplicación Slim respeta tu opcion `error_reporting` existente.
* Una aplicación Slim solo maneja errores y excepciones generadas dentro de la aplicación Slim;
* Una aplicación Slim convierte los errores en objetos `ErrorException` y los lanza;
* Una aplicación Slim usa su manejador de errores incorporado si su opción `debug` es `true`; de otra manera, 
utiliza el manejador de errores personalizado.
