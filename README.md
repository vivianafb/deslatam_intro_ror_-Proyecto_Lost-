# Requisitos

Este tutorial asume lo siguiente

* Tienes instalado Bootstrap 3 a través de la sección (a) del [README de Bootstrap for Sass](https://github.com/twbs/bootstrap-sass).

* Se ocupará el pre procesador de CSS ,[Sass](https://sass-lang.com/guide), para la escritura y manejo de CSS. Más detalles en [¿Qué es Sass?](https://www.creativebloq.com/web-design/what-is-sass-111517618).

* Se usa [Rails-layout](https://github.com/RailsApps/rails_layout) para reemplazar layouts/application.html.erb para aplicar los estilos de Bootstrap y generar las vistas de devise. Instalar normalmente como una gema y ejecutar el comando indicado. Leer la sección **The “layout:install” Command** para un mejor entendimiento de lo que sucede.

```
rails generate layout:install bootstrap3
```

* Turbolinks fueron removidos. [Tutorial](http://codkal.com/rails-how-to-remove-turbolinks/).

* [Font Awesome](https://github.com/FortAwesome/font-awesome-sass) para íconos awesome :).

# Estado del proyecto

Este proyecto es un proyecto base que contempla los siguientes elementos aplicados y funcionalidades:

## Elementos Aplicados

1. Se instaló Bootstrap versión 3.3.7 para poder integrarlo utilizando Sass. Sin embargo, para hacer su uso más simple se eliminó el archivo creado **1st_load_framework.css.scss** por la gema Rails Layout indicado en la sección **The “layout:install” Command** y se utilizó el archivo **app/assets/stylesheets/application.scss** para importar bootstrap.

2. Existe una barra superior responsiva con las secciones HOME y Users.

3. Existe la sección de perfil del usuario para hacer sign up (registrarse), sign in (iniciar sesión) y sign out (cerrar sesión).

## Funcionalidades

1. Página inicial de bienvenida donde solo los usuarios visitantes (no registrados ni logeados) pueden visitar

2. Se creará un sistema básico para crear usuarios a través de [Scaffold](http://guides.rubyonrails.org/v3.2.9/getting_started.html#getting-up-and-running-quickly-with-scaffolding) de Rails. Esto quiere decir que se puede hacer el [CRUD](https://es.wikipedia.org/wiki/CRUD) de usuarios en la aplicación. Sólo los usuarios logeados pueden acceder a esta funcionalidad.

# La gema Devise

Este proyecto se divide en varios branchs para que se pueda visualizar cómo se puede aplicar Devise paso a paso sobre un proyecto que tiene una librería como Bootstrap aplicado. Los branch son:

## Branch 01: 01_devise_instalado 

Proyecto rails con todos los [elementos aplicados](https://github.com/enaguero/devise_rails/tree/01_devise_instalado#elementos-aplicados). Solo contempla la incorporación de la gema Devise, la instalación de Devise, agregar devise al modelo User y la generación de Scaffold del modelo User. Los comandos asociados son:

```
$ rails generate devise:install
$ rails g scaffold User name:string last_name:string phone:string address:string
$ rails generate devise User
```

En este branch se puede acceder a todas las secciones, se puede tratar de registrar usuarios solo con email y password, se pueden visualizar en la lista general, sin embargo, no se verán campos debido a que no se configurado los campos adicionales para ser parte del proceso de registro de Devise. Es posible hacerlo desde el inicio, sin embargo, es una decisión de diseño en qué momento crearlos junto al usuario y sus sesiones.  

Por último, para saber las rutas disponibles que nos entrega Devise es posible hacerlo a través de la consola con el comando:

```
$ rake routes
```

Las rutas de devise vienen dadas por el código **devise_for :users** en el archivo routes `<name_app>/config/routes.rb` y las rutas agregadas vienen por los siguientes [módulos agregados](https://www.rubydoc.info/github/plataformatec/devise/) en el modelo User:

1. :database_authenticatable
2. :registerable
3. :recoverable
4. :rememberable
5. :trackable
6. :validatable 

Para más detalle de como iniciar con Devise, ver la [documentación oficial de Devise](https://github.com/plataformatec/devise#getting-started).

## Branch 02: 02_manejo_de_sesiones

La gema Devise ha estado en el mundo Rails desde el 2009 y se ha convertido en ya casi un estándar al momento de realizar todo el proceso de registro y manejo de sesiones en Rails. Sin embargo, es siempre bueno saber cómo una implementación hecha la podemos utilizar a nuestro favor sabiendo que élementos posicionar.

El objetivo de esta segunda parte es poder realizar lo siguiente:

1. Al momento de visitar la página inicial el sistema identifique si el usuario está ha iniciado sesión, si no ha iniciado sesión mostrar la barra con los botones Home, Iniciar Sesión y Registrar (pero registrar como sub menú).

2. Controlar el acceso de los usuarios permitiendo que sólo los usuarios registrados puedan visitar el panel de usuarios creados vía Scaffold.

## Branch 03: 03_agregar_nuevos_campos

El objetivo de este branch es poder agregar nuevos campos a los que Devise trae por defecto (email, password, password_confirmation) tales como nombre (name), apellido (last_name) y dirección (address) al momento de registrar (crear) un usuario en la plataforma. Esto se realiza a través de los siguientes pasos:

1. Incorporar nuevos parámetros en el formulario de creación/registro (sign up) de un usuario.
2. Incorporar los nuevos parámetro para que sean procesados por los [**strong params**](http://api.rubyonrails.org/v5.0/classes/ActionController/StrongParameters.html) de rails.
3. El formulario de registro se posiciona en la página de inicio

# Fuentes

1. [Ícono de usuario para foto de perfil](http://jsfiddle.net/bJcrk/2/).
2. [Iniciar con Devise - Documentación Oficial](https://github.com/plataformatec/devise#getting-started).