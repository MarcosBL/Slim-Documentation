---
title: Métodos de ayuda del Request
status: live
---

El objeto request de la aplicación Slim provee varios métodos de ayuda para obtener información HTTP comun:

### Tipo de Contenido

Obtener el tipo de contenido del request (por ejemplo "application/json;charset=utf-8"):

    <?php
    $req = $app->request;
    $req->getContentType();

### Tipo de Media

Obtener el tipo de media del request (por ejemplo "application/json"):

    <?php
    $req = $app->request;
    $req->getMediaType();

### Parámetros del Tipo de Media

Obtener los parámetros del tipo de media del request (por ejemplo [charset => "utf-8"]):

    <?php
    $req = $app->request;
    $req->getMediaTypeParams();

### Charset del Contenido

Obtener el character set del contenido del request (por ejemplo "utf-8"):

    <?php
    $req = $app->request;
    $req->getContentCharset();

### Longitud del Contenido

Obtener la longitud del contenido del request:

    <?php
    $req = $app->request;
    $req->getContentLength();

### Host

Obtener el host del request (por ejemplo "slimframework.com"):

    <?php
    $req = $app->request;
    $req->getHost();

### Host con Puerto

Obtener el host del request con el puerto (por ejemplo "slimframework.com:80"):

    <?php
    $req = $app->request;
    $req->getHostWithPort();

### Puerto

Obtener el puerto del request (por ejemplo 80):

    <?php
    $req = $app->request;
    $req->getPort();

### Esquema

Obtener el esquema del request (por ejemplo "http" o "https"):

    <?php
    $req = $app->request;
    $req->getScheme();

### Ruta

Obtener la ruta del request (URI raíz + URI del recurso):

    <?php
    $req = $app->request;
    $req->getPath();

### URL

Obtener el URL del request (esquema + host [ + puerto si no es estandar ]):

    <?php
    $req = $app->request;
    $req->getUrl();

### Dirección IP

Obtener la dirección IP del request:

    <?php
    $req = $app->request;
    $req->getIp();

### Referidor

Obtener el referidor del request:

    <?php
    $req = $app->request;
    $req->getReferrer();

### User Agent

Obtener el user agent del request como string:

    <?php
    $req = $app->request;
    $req->getUserAgent();
