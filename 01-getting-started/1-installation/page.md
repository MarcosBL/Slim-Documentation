---
title: Instalación
status: live
---

### Instalación con Composer

Instalar composer en tu proyecto:

    curl -s https://getcomposer.org/installer | php

Crear el archivo `composer.json` en la raíz de tu proyecto:

    {
        "require": {
            "slim/slim": "2.*"
        }
    }

Instalar con composer:

    php composer.phar install

Agrega ésta línea en el archivo `index.php` de tu aplicación:

    <?php
    require 'vendor/autoload.php';

### Instalación Manual

Descarga y extrae Slim Framework en la carpeta de tu proyecto y usa `require` 
para agregarlo en el archivo `index.php`. También vas a necesitar registrar el 
autoloader de Slim.

    <?php
    require 'Slim/Slim.php';
    \Slim\Slim::registerAutoloader();
