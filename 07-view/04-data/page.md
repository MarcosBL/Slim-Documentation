---
title: Datos de la Vista
status: live
---

<div class="alert alert-info">
    <strong>¡Información!</strong> No será habitual que fijes o añadas datos
	directamente al objeto vista. Por lo general, pasarás datos a la vista a través 
	del método `render()` de la aplicación Slim.
    Dale un ojo a <a href="/pages/view-rendering-templates">Renderizando Plantillas</a>.
</div>

Los métodos del objeto vista `setData()` y `appendData()` inyectan datos 
en el objeto vista; los datos inyectados estarán disponibles para las plantillas 
de vista. Internamente, datos de la Vista se almacenan en un array clave-valor.

### Asignando Datos

El método de instancia `setData()` del objeto vista sobreescribirá los datos ya 
existentes. Utilizaremos este método para asignar un solo valor a una sola variable:

    <?php
    $app->view->setData('color', 'red');

Los datos de la vista contendrán ahora una clave “color” con el valor “red”. 
También puedes utilizar el método de vista `setData()` para asignar un array 
completo de datos de una sola vez:

    <?php
    $app->view->setData(array(
        'color' => 'red',
        'size' => 'medium'
    ));

Recuerda, el método `setData()` sobreescribirá los datos ya existentes.

### Añadiendo Datos

El objeto vista también dispone de un método `appendData()` que añade datos 
a los ya existentes en la vista. Este método acepta un array como único parámetro:

    <?php
    $app->view->appendData(array(
        'foo' => 'bar'
    ));
