---
title: Grupos de Ruta
status: live
---

Slim te permite agrupar rutas relacionadas. Esto es útil cuando te encuentras repitiendo los mismos 
segmentos de URL para múltiples rutas. Esto es mejor explicado con un ejemplo. Pretendamos que estamos 
construyendo un API para libros.

    <?php
    $app = new \Slim\Slim();

    // Grupo API
    $app->group('/api', function () use ($app) {

        // Grupo Library
        $app->group('/library', function () use ($app) {

            // Obtener libro con ID
            $app->get('/books/:id', function ($id) {

            });

            // Actualizar libro con ID
            $app->put('/books/:id', function ($id) {

            });

            // Borrar libro con ID
            $app->delete('/books/:id', function ($id) {

            });

        });

    });

Las rutas definidas arriba sera accesibles respectivamente en:

    GET    /api/library/books/:id
    PUT    /api/library/books/:id
    DELETE /api/library/books/:id

Los grupos de ruta son muy útiles para agrupar rutas relacionadas y evitar repetir segmentos 
URL comunes en cada definición de ruta.
