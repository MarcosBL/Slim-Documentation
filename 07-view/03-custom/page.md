---
title: Vistas a medida
status: live
---

Una aplicación Slim delega el renderizado de plantillas a su objeto vista. Una vista
a medida es una subclase de `\Slim\View` que implementa esta interfaz:

    <?php
    public render(string $template);

El método `render` del objeto vista debe devolver el contenido renderizado 
de la plantilla especificada por su parámetro `$template`. Cuando se llama al 
método render de una vista a medida, se le indica la ruta a plantilla deseada 
(relativa a la configuración “templates.path” de la aplicación Slim) como parámetro. 
Aquí tienes un ejemplo de vista a medida:

    <?php
    class CustomView extends \Slim\View
    {
        public function render($template)
        {
            return 'The final rendered template';
        }
    }

La vista a medida puede hacer lo que quiera internamente mientras devuelva la 
salida de la plantilla renderizada como cadena de texto. Una vista a medida hace 
que sea sencillo integrar sistemas PHP de plantillas como Twig o Smarty.

<div class="alert alert-info">
    <strong>¡Atención!</strong> Una plantilla a medida puede acceder a los datos 
	que le facilita el método <code>render()</code> de la aplicación Slim con 
	<code>$this->data</code>.
</div>

Puedes ojear vistas listas para su uso que trabajan con motores de plantillas PHP famosos en el repositorio de GitHub Slim-Extras.

### Vista de Ejemplo

    <?php
    class CustomView extends \Slim\View
    {
        public function render($template)
        {
            // $template === 'show.php'
            // $this->data['title'] === 'Sahara'
        }
    }

### Ejemplo de Integración

Si la vista a medida no puede ser detectada por un autoloader registrado, 
debemos requerirla antes de que la aplicación Slim se instancie.

    <?php
    require 'CustomView.php';

    $app = new \Slim\Slim(array(
        'view' => new CustomView()
    ));

    $app->get('/books/:id', function ($id) use ($app) {
        $app->render('show.php', array('title' => 'Sahara'));
    });

    $app->run();
