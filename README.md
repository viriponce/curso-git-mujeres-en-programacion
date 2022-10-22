
## Curso introductorio a git y GitHub ##

Bienvenidas al curso introductorio a git y GitHub. Este repositorio acompañará las lecciones que se realizarán cada sábado, y el contenido se irá actualizando a medida que avance el curso.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
Si durante el curso tienes dudas o algún problema, pide ayuda en el chat o escríbeme a ocallaghanpatty@gmail.com

...¡comencemos!

Instalando git
--------------

Sigue las siguientes instrucciones, dependiendo de tu sistema operativo: [Instalación de Git](https://git-scm.com/book/es/v2/Inicio---Sobre-el-Control-de-Versiones-Instalaci%C3%B3n-de-Git).

Setup
-----

Lo primero que debemos hacer es configurar nuestros datos básicos: nombre y email. De esta manera, podemos identificar las contribuciones al proyecto de cada uno de los participantes.

    $ git config --global user.name "Tu Nombre"
    $ git config --global user.email tu.email@ejemplo.com


¡Empecemos!
-----------

En primer lugar, clona este repositorio con el comando `git clone`:

    $ git clone https://github.com/pattyneta/curso-git-mujeres-en-programacion.git
    
También puedes crear una copia del repositorio directamente en github. Puedes conseguir
el botón de "Fork" en la esquina superior derecha de la pantalla en el repositorio que quieres clonar,
puedes conseguir más información al respecto [aquí](https://help.github.com/articles/fork-a-repo/).

Luego de clonar el repositorio, deberías tener un directorio llamado `curso-git-mujeres-en-programacion`. Este es tu `working directory`

    $ cd curso-git-mujeres-en-programacion
    $ ls

Git también crea un subdirectorio adicional llamado `.git`. Aquí es
donde se guardan todos los datos y el historial de tu repositorio.

    $ ls -a .git

Verás los siguientes directorios:

    branches  config  description  HEAD  hooks  info  objects  refs

El area de "Staging"
--------------------

Ahora, vamos a añadir algunos archivos al repositorio. Para esto vamos a usar el comando `touch` para crearlos.

Vamos a crear dos archivos llamados `cancionfavorita.txt` y `librofavorito.txt`.

    $ touch cancionfavorita.txt librofavorito.txt

Ahora, vamos a añadir estos archivos al area de Staging

    $ git add cancionfavorita.txt librofavorito.txt

Haciendo el commit
------------------

Ahora estamos listas para ejecutar el commit. La opción `-m` permite agregar un mensaje descriptivo al commit.

    $ git commit -m "Agregando dos archivos"

¿Qué ha pasado?
---------------

Ahora debemos tener un nuevo commit. Para ver todos los commits que hemos hecho, se usa el comando
`git log`

    $ git log

El log muestra todos los commits listados desde el más reciente al más antiguo. 
Verás varios datos como el nombre del autor, la fecha en que se realizón, un número SHA de confirmación, y el mensaje.

También deberías ver tu commit más reciente, donde añadiste los dos nuevos archivos
en la sección anterior. Sin embargo, `git log` no muestra los archivos
asociados a cada commit. Para ver más información sobre un commit, utiliza
`git show`.

    $ git show

Debes ver algo similar a:

    commit bba8b163894be6ae8bda75df24b1c1732505ed8a
    Author: Patty O'Callaghan <ocallaghanpatty@gmail.com> 
    Date:   Sun Oct 1 13:32:55 2022 +1200

        Agregando dos archivos

    diff --git a/cancionfavorita.txt b/cancionfavorita.txt
    new file mode 100644
    index 9713636ef..a70e78c60
    diff --git a/librofavorito.txt b/librofavorito.txt
    new file mode 100644
    index 9713636ef..a70e78c60

Agregando contendido
--------------------

Ahora, vamos a agregar contenido a los archivos.

Abre `cancionfavorita.txt` y escribe una línea de tu canción favorita:

Ejemplo: Cuando la tarde languidece renacen las sombras y en la quietud los cafetales vuelven a sentir.

Luego, guarda el archivo.

¿Cómo podemos saber qué cambiamos? Para esto, usamos `git diff`. Esto es muy útil para ver exactamente que los cambios que hicimos.

    $ git diff
    
Debes ver algo como esto:

    diff --git a/cancionfavorita.txt b/cancionfavorita.txt
    index a32be17..6cddbae 100644
    --- a/cancionfavorita.txt
    +++ b/cancionfavorita.txt
    @@ -0,0 +1 @@
    +Cuando la tarde languidece renacen las sombras y en la quietud los cafetales vuelven a sentir.

Vamos de nuevo al area Staging
------------------------------

Ahora agrega los cambios en el archivo `cancionfavorita.txt` al area de Staging. ¿Recuerdas cómo?

Ahora, chequea el `status` de `cancionfavorita.txt`. ¿Está ahora en el area de Staging?

Deshaciendo
-----------

Digamos que lo pensaste mejor, y lo que agregaste en el archivo no es realmente tu canción favorita. Una
ventaja del area de Staging es que nos permite retroceder antes de que ejecutemos el commit - lo cual es un poco más difícil de revertir. Recordando la analogía del correo es más fácil sacar el correo de la caja de cartón antes de sellarlo que después.

Para "sacar" el archivo del area de Staging debemos ejecutaqr:

    $ git reset HEAD alice.txt

    Unstaged changes after reset:
    M   cancionfavorita.txt

Compara el `git status` de ahora con el anterior. ¿En qué se diferencia?

El area de Staging debería estar ahora vacía. ¿Qué ha pasado con los cambios que agregamos al archivo de tu canción favorita? Siguen ahí. Ahora hemos vuelto al estado justo antes de añadir este archivo al area de Staging. 

Deshaciendo - Parte II
----------------------

A veces no nos gusta lo que hemos hecho y deseamos volver al
el último estado *grabado*. En este caso, queremos volver al estado
justo antes de añadir el texto a `cancionfavorita.txt`.

Para lograr esto, usamos `git checkout`:

    $ git checkout cancionfavorita.txt

Ahora se han deshecho los cambios. Tu archivo debe estar ahora vacío.

Más sobre Commits
-----------------

Ahora, hablaremos un poco sobre la idea de commits convencionales. Puedes leer más sobre el tema [aquí](https://www.conventionalcommits.org/es/v1.0.0/).

Branching
---------

La mayoría de las grandes bases de código o code baases tienen al menos dos ramas: una rama "activa" y una
rama "de desarrollo". La rama activa contiene el código que está bien para ser desplegado
en un sitio web, o descargado por los clientes. La rama de desarrollo
permite a los desarrolladores trabajar en características que podrían no estar libres de errores. Sólo
una vez que todos estén contentos con la rama de desarrollo, se fusionará
con la rama activa.

Crear una rama o branch en Git es fácil. El comando `git branch`, cuando es usado sin opciones adicionales, muestra todas las ramas que tienes en tu repositorio:

    $ git branch

El caracter `*` debe mostrar la rama en la que te encuentras actualmente, la cuál es `master`.

Si quieres crear una nueva rama, debes ejecutar
`git checkout -b (nombre-nueva-rama)` :

    $ git checkout -b exp1

Ejecuta `git branch` nuevamente para chequear en que rama te encuentras:

    $ git branch
      exp1
    * master

La nueva rama o branch ha sido creada. Ahora, trabajemos en esta rama. Para cambiar a la nueva rama debemos ejecutar:

    $ git checkout exp1

`git checkout (nombre-rama)` se usa para cambiar de rama.

Ahora, agreguemos un archivo en la nueva rama,

    $ echo 'Aprendiendo en mi curso de git' > test.txt
    $ git add test.txt
    $ git commit -m "Agregando un archivo de prueba"

Ahora, comparemos el contenido de nuestra rama con el contenido de la rama master. Para esto usaremos `git diff`

    $ git diff master

Básicamente lo que arroja el comando luego de ser ejecutado es que `test.txt` está presente en
la rama `exp1`, pero está ausente en la rama `master`.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Help-browser.svg/20px-Help-browser.svg.png)
¿Problemas? Pide ayuda en el chat o escríbeme a ocallaghanpatty@gmail.com

