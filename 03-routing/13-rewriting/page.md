---
title: Reescritura del URL de Ruta
status: live
---

Les recomiendo firmemente usar un servidor web que soporte reescritura de URLs; esto te permitirá disfrutar de URLs 
limpias y amigables para humanos en tu aplicación Slim. Para habilitar la reescritura de URLs, debes usar las herramientas 
apropiadas provistas por tu servidor web para reenviar todos los request HTTP al archivo PHP en donde instancias y corres 
la aplicación Slim. Los siguientes son configuraciones de ejemplo mínimas para Apache con mod_php y nginx. Estas no deberían 
ser usadas como configuración de aplicaciones en producción pero deberían ser suficiente para darte una idea. Para saber mas 
sobre despliegue de servidor en general puedes continuar leyendo en <http://www.phptherightway.com>.

### Apache y mod_rewrite

Este es un ejemplo de una estructura de directorios:

    /path/www.mysite.com/
        public_html/ <-- Raíz de documento!
            .htaccess
            index.php <-- Instancio Slim aquí!
        lib/
            Slim/ <-- Almaceno los archivos de la librería Slim aquí!

El archivo **.htaccess** en la estructura de directorio de arriba contiene:

    RewriteEngine On
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteRule ^ index.php [QSA,L]

También necesitas una directiva de directorio para habilitar archivos **.htaccess** y permitir que la directiva 
**RewriteEngine** sea usada. Esto es hecho por lo general globalmente en el archivo **httpd.conf**, pero generalmente 
es buena idea limitar la directiva solo para tu host virtual encerrándola en tu bloque de configuración **VirualHost**. 
Esto es hecho generalmente en tu configuración de la siguiente forma:

    <VirtualHost *:80>
        ServerAdmin me@mysite.com
        DocumentRoot "/path/www.mysite.com/public_html"
        ServerName mysite.com
        ServerAlias www.mysite.com

        #ErrorLog "logs/mysite.com-error.log"
        #CustomLog "logs/mysite.com-access.log" combinado

        <Directory "/path/www.mysite.com/public_html">
            AllowOverride All
            Order allow,deny
            Allow from all
        </Directory>
    </VirtualHost>

Como resultado, Apache enviará todas las peticiones a archivos no existentes a mi script **index.php** en donde 
instancio y corro mi aplicación Slim. Con la reescritura de URL habilitado y asumiendo que la aplicación Slim es 
definida en **index.php**, puedes acceder a la ruta de aplicación de abajo en “/foo” en lugar de “/index.php/foo”.

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () {
        echo "Foo!";
    });
    $app->run();

### nginx

Usaremos la misma estructura de directorio que en el ejemplo anterior, pero con nginx nuestra configuración estará 
en el archivo **nginx.conf**.

    /path/www.mysite.com/
        public_html/ <-- Raíz de documento!
            index.php <-- Instancio Slim aquí!
        lib/
            Slim/ <-- Almaceno los archivos de la librería Slim aquí!

Este es una muestra de un archivo **nginx.conf** en donde usamos la directiva **try_files** para servir el archivo si existe, 
bueno para archivos estáticos (imágenes, css, js etc), y de otra manera lo reenviamos al archivo **index.php**. 

    server {
        listen       80;
        server_name  www.mysite.com mysite.com;
        root         /path/www.mysite.com/public_html;

        try_files $uri /index.php;

        # esto solo pasara index.php al proceso fastcgi lo cual es mas seguro generalmente
        # pero asume que todo el sitio es corrido con Slim.
        location /index.php {
            fastcgi_connect_timeout 3s;     # el valor por defecto de 60s es muy largo
            fastcgi_read_timeout 10s;       # el valor por defecto de 60s es muy largo
            include fastcgi_params;
            fastcgi_pass 127.0.0.1:9000;    # asume que estas corriendo php-fpm localmente en el puerto 9000
        }
    }

La mayoría de las instalaciones tendrán un archivo **fastcgi_params** por defecto puesto en marcha que puedes incluir 
como se muestra arriba. Algunas configuraciones no incluyen el parámetro **SCRIPT_FILENAME**. Debes asegurar que incluyes 
este parámetro o puedes terminar con un error de Ningún archivo de entrada del proceso fastcgi. Esto puede hacerse directamente 
en el bloque location o simplemente agregándolo al archivo **fastcgi_params**. De cualquier manera se ve algo así:

    fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;

### Sin reescritura de URL

Slim trabajara sin reescritura de URL. En este escenario, debes incluir el nombre del archivo en donde instancias 
y corres la aplicación Slim en el URI de recurso. Por ejemplo, asumiendo que la siguiente aplicación Slim es definida en 
**index.php** en el nivel mas alto de la raíz de documento de tu host virtual:

    <?php
    $app = new \Slim\Slim();
    $app->get('/foo', function () {
        echo "Foo!";
    });
    $app->run();

Puedes acceder a la ruta predefinida en “/index.php/foo”. Si la misma aplicación es definida en su lugar en 
el archivo **index.php** dentro del directorio blog/, puedes acceder a la ruta definida en /blog/index.php/foo.
