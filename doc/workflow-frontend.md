I2B Frontend WorkFlow
===

**Adaptado para Proyectos I2B.cl**

Este es un sencillo flujo que pueden utilizar para proyectos frontend. Debes tener lo fundamental para funcionar:

- [NodeJS](http://nodejs.org/download/)
- [Browsersync](https://browsersync.io/docs/gulp)
- *Gulp command line interface* (CLI): se instala a través del comando de terminal:
```
$ sudo npm install gulp-cli -g
$ sudo npm install gulp -D
```
- [GIT](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Ruby](https://www.ruby-lang.org/en/documentation/installation/)
- [Sass](http://sass-lang.com/install)
```
$ sudo gem install sass
```

**Atención usuarios de Windows**, necesitas un poco más de cuidado para configurar todo correctamente [Leer más en la Wiki](https://github.com/I2BTech/i2b-frontend-workflow/wiki/Problemas-en-Windows)

### TL;DR (resumen) ###

1. Descargar .zip de [I2B Frontend WorkFlow](https://git.i2btech.com/i2b/front-components/repository/archive.zip?ref=master)
2. Moverlos a su directorio de trabajo local (por ej. localhost/proyecto)
3. `$ npm install` (instala node packages)
4. `$ gulp`
5. fin!

### package.json ###

Es el archivo que contiene los nombres de las librerías **Node** que utilizaremos para automatizar nuestras tareas recurrentes y que reside en la raíz del proyecto. Aquí están el nombre y la versión de cada plugin que necesitaremos, de una larga lista de plugins existentes.

Se necesita cambiar al inicio de este archivo el *Nombre-Cliente-y-Proyecto* (sin espacios ni caracteres especiales):

	{
		"name": "Nombre-Cliente-y-Proyecto"
		...

### Gulpfile.js ###

Es el archivo base con el cual crearemos las tareas que necesitamos corra **GulpJS** por nosotros y que reside en el folder runner/ del proyecto junto a **package.json**. En este archivo están definidas los plugins que utilizaremos y cómo deben trabajar, en esta ocasión incluyo los siguientes:

- **concat**: concatena y minifica librerías JavaScript
- **uglify**: minifica archivos JavaScript
- **spritesmith**: crea una imagen y una hoja de estilos sprite a partir de varios íconos
- **imagemin**: comprime imágenes
- **pug**: compila y minifica archivos .pug
- **sass**: compila y minifica archivos .scss
- **typescript**: compila archivos .ts
- **watch**: corre tareas definidas cada vez que se realizan cambios a ellas, en este caso todas las anteriores.
- **autoprefixer**: agrega prefijos directo a los archivos CSS generados de SCSS dentro de `dev/css` correspondientes a las últimas 3 versiones (la actual y una anterior) de los principales browsers y las versiones en específico de IE 8 y 9.
- **Test Js Karma**: verifica sintaxis JS según reglas básicas definidas en `karma.conf.js` respectivamente.

### Uso ###

El directorio base se llama `/proyecto` y contiene todo lo necesario para comenzar a trabajar. Suponiendo que trabajas en un servidor local, la estructura básica de archivos es la siguiente:

	/proyecto/runner/Gulpfile.js
	/proyecto/runner/package.json
	/proyecto/dev/index.html


El directorio donde trabajarás tus assets se llama `/source ` y contiene:

	/proyecto/source/ts/
	/proyecto/source/js/
	/proyecto/source/js/ie/
	/proyecto/source/sass/
	/proyecto/source/sass/inc/
	/proyecto/source/sass/components/
	/proyecto/source/sass/partial/
	/proyecto/source/pug/
	/proyecto/source/pug/inc/
	/proyecto/source/pug/components/
	/proyecto/source/pug/partial/
	/proyecto/source/images/
	/proyecto/source/images/sprites/


Los que después de procesados por **GulpJS** residirán en `/dev` y son los que debes llamar desde tus archivos **HTML**:

	/proyecto/dev/js/
	/proyecto/dev/js/ie/
	/proyecto/dev/css/
	/proyecto/dev/img/

Para comenzar a trabajar, en Terminal/Consola debes estar en el directorio que estés trabajando:

	$ cd /path/to/proyecto/

Para instalar los plugins a utilizarse y que están definidos en **package.json**:

	$ sudo npm install

Con esto se llamarán a todos los repositorios e instalará los paquetes necesarios para hacer las tareas que tenemos asignadas. Esto puede tomar unos minutos y creará un directorio `/node_modules` en la raíz de tu proyecto. Este directorio sólo le es útil a **GulpJS**, no debemos utilizarlo en ambiente productivo.

Antes de correr **GulpJS**, abre **Gulpfile.js** y revisa los path que concuerden con los que estés trabajando. Si todo concuerda, acciona el comando:

	$ gulp

![](http://www.csslab.cl/wp-content/uploads/2014/04/2watch.png)

El cual comenzará a procesar las tareas ya definidas. En este momento debes llamar el directorio de trabajo en tu browser (a través de tu servidor web local) y activar **Browsersync**. Cuando el ícono cambie es porque está sincronizado con **GulpJS** y a cada cambio en archivos **pug/, sass/, img/, ** en tu proyecto, **watch** hará que se actualicen los archivos y **Browsersync** recargará el browser por tí.

### Test ###

A través de un nueva tarea de **GulpJS** se prueba el archivo **JavaScript** en búsqueda de errores de sintaxis y mejoras en él:

	$ gulp test

Además se rastrea los archivos `.html` generados desde `.pug` buscando errores de sintaxis básicos automáticamente a través de **watch** y manualmente con el comando:

	$ gulp test


**Happy Coding :)**


#### To-Do: ####

- Task para performance
