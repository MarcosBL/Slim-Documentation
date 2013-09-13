---
title: Métodos de Request
status: live
---

Cada request de HTTP tiene un método (por ejemplo GET o POST). Puedes obtener el método actual del request 
HTTP por vía del objeto request de la aplicación Slim:

    /**
     * ¿Cual es el método de request?
     * @return string (por ejemplo GET, POST, PUT, DELETE)
     */
    $app->request->getMethod();

    /**
     * ¿Es este un request GET?
     * @return bool
     */
    $app->request->isGet();

    /**
     * ¿Es este un request POST?
     * @return bool
     */
    $app->request->isPost();

    /**
     * ¿Es este un request PUT?
     * @return bool
     */
    $app->request->isPut();

    /**
     * ¿Es este un request DELETE?
     * @return bool
     */
    $app->request->isDelete();

    /**
     * ¿Es este un request HEAD?
     * @return bool
     */
    $app->request->isHead();

    /**
     * ¿Es este un request OPTIONS?
     * @return bool
     */
    $app->request->isOptions();

    /**
     * ¿Es este un request PATCH?
     * @return bool
     */
    $app->request->isPatch();

    /**
     * ¿Es este un request XHR/AJAX?
     * @return bool
     */
    $app->request->isAjax();
