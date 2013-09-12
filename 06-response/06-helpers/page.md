---
title: Helpers de la Respuesta
status: live
---

El objeto respuesta nos facilita algunos métodos de ayuda para inspeccionar e 
interactuar con la respuesta HTTP subyacente.

### Finalización

El método `finalize()` del objeto respuesta devuelve un array numérico consistente 
en `[status, header, body]`. El status es un entero; el header es una estructura 
de datos iterable; y el body es una cadena de texto. Una vez creado un objeto tipo 
`\Slim\Http\Response` en tu aplicación Slim o en su middleware, podrías llamar 
al método `finalize()` del objeto respuesta para generar el status, header, y 
de la respuesta HTTP subyacente.

    <?php
    /**
     * Preparamos un nuevo objeto response
     */
    $res = new \Slim\Http\Response();
    $res->setStatus(400);
    $res->write('You made a bad request');
    $res->headers->set('Content-Type', 'text/plain');

    /**
     * Finalize
     * @return [
     *     200,
     *     ['Content-type' => 'text/plain'],
     *     'You made a bad request'
     * ]
     */
    $array = $res->finalize();

### Redirección

El método `redirect()` del objeto respuesta asignará el correspondiente status y 
su cabecera **Location:** necesaria para devolver una respuesta **3xx Redirect**.

    <?php
    $app->response->redirect('/foo', 303);

### Análisis del Status

El objeto respuesta provee otros métodos de ayuda para inspeccionar su estado 
actual. Todos los métodos siguientes devuelven un valor booleano:

    <?php
    $res = $app->response;

    //Se trata de respueta informativa?
    $res->isInformational();

    //Se trata de una respuesta 200 OK?
    $res->isOk();

    //Se trata de una respuesta 2xx exitosa?
    $res->isSuccessful();

    //Se trata de una respuesta de redirección 3xx?
    $res->isRedirection();

    //Se trata de una respuesta de redirección específica? (301, 302, 303, 307)
    $res->isRedirect();

    //Se trata de una respuesta prohibida?
    $res->isForbidden();

    //Se trata de una respuesta No encontrado?
    $res->isNotFound();

    //Se trata de una respuesta de error del cliente?
    $res->isClientError();

    //Se trata de una respuesta de error del servidor?
    $res->isServerError();
