+++
author = ["Jesus R. Gonzalez L."]
date = "2019-11-28T00:00:00-08:00"
title = "Como construir sitios web con HUGO"
series = ["Tutorial"]
draft = true
+++

    Esta publicación tiene como objetivo enseñar como construir sitios web utilizando HUGO y como subirlo a un hosting.

Hugo es un generador de sitios web estáticos construidos con el lenguaje GO, fue creado en el año 2013. Con él se puede generar sitios web en poco tiempo, versátiles y muy rapidos de hecho su lema: "The world’s fastest framework for building websites".  Algunos casos notables donde se utiliza HUGO son:

- <https://kubernetes.io/>
- <https://www.netlify.com/>
- <https://www.smashingmagazine.com/>
- <https://developers.cloudflare.com/>
- <https://litecoin.org/>

Para trabajar con Hugo primeramente necesitamos instalar en nuestra maquina los siguientes requerimientos:

1. Git
2. Go (mayor que Go 1.11)
3. Chocolatey. (Para esta publicación utilizare Windows 7, por ende es necesario trabajar con Chocolatey, HUGO tambien tiene instrucciones para instalarse en otros sistemas operativos deberias revisar en este link:
<https://gohugo.io/getting-started/installing/#quick-install>
).

### Instalación de Git:</h4>

Para instalar git debemos primeramente descargarlo en el siguiente link: <https://git-scm.com/downloads,> luego viene el proceso de instalación. Cuando se haya finalizado la instalacion abrimos Git Bash y verificamos que todo el proceso de instalación fue exitoso.

Introducimos en la consola el siguiente comando:

    git --version

Si no muestra ningun error en su instalación debería mostrar la versión de GIT que fue instalada.

### Instalación de Golang(GO)

Es necesario instalar Go para el funcionamiento de HUGO, primero se debe descargar de la pagina oficial: <https://golang.org/dl/.>

Luego de haber sido descargado pasamos a el proceso de instalación de GO. Cuando haya finalizado la instalacion debemos agregar una variable en Enviroment Variables –> User Variables con el nombre de GOPATH  y en la seccion value la dirección de la carpeta donde se instalo GO.
Ya con eso se podrá desde la consola ingresar los comandos de GO. Para validar que la instalación fue exitosa ingresa el siguiente comando:

    go version

El cual debería mostrar la versión de Go instalada en su computadora.

### Instalacion de Chocolatey

Chocolatey es un manejador de paquetes de windows. Su instalación es bastante sencilla, primeramente hay que asegurarse de abrir powershell.exe como administrador de lo contrario no se instalara.

Ahora toca ingresar el siguiente comando en la consola:

    Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

Debemos esperar unos segundos, para que se descarguen los componentes necesarios y luego se instalen automaticamente. En la consola no debe aparecer error para validar que su instalación fue correcta agregue el siguiente comando:

    choco  /?

En la consola de powershell luego que ingreso el comando de arriba debería mostrar la versión instalada de chocolatey.

Ahora si pasamos a la parte que es enfocada en HUGO.

Lo primero que debemos hacer es dirigirnos donde se crearan la carpeta de tu proyecto, abrir la consola Git Bash de modo administrador en esa carpeta. Ya abierta la consola podemos ingresar el siguiente comando que se encarga de instalar HUGO:

    choco install hugo

luego que haya finalizado la instalación podemos verificar que se instalo correctamente ingresando ingresando el comando:

    hugo Version

Mostrando la versión del hugo que se instalo.
Ahora pasaremos a crear nuestro proyecto le podemos agregar el nombre que sea más adecuado a lo que desees hacer, con el siguiente comando:

    hugo new site nombre_tu_preferencia

ejemplo:

    hugo new site gopherblog

Luego podrá ver que se creo una carpeta con el nombre que le coloco a su proyecto. Debemos dirigirnos a la carpeta del archivo que se creo con el comando anterior colocando en la consola:

    cd gopherblog

ahora iniciamos git en la carpeta de nuestro proyecto con el comando:

    git init

ese comando inicia un repositorio git en el proyecto.

debemos agregar un tema para nuestro proyecto, para este tutorial utilizare el tema: hugo-sustain.
Nota: Hugo posee distintos temas para distintos usos.

Con el siguiente comando vamos a clonar el tema que se eligio y guardarlo en la carpeta "themes" de nuestro proyecto.

    git clone https://github.com/nurlansu/hugo-sustain.git themes/hugo-sustain

Luego que haya finalizado la clonacion podemos ver en la carpeta themes que se encuentra una carpeta con el nombre hugo-sustain donde se clono el repositorio del tema.

Para empezar a trabajar con el tema lo primero que necesitamos hacer es modificar el archivo "config.toml" de nuestro proyecto, en ese archivo podemos modificar variables usados en el template.

Debemos empezar por agregar el tema a usar:

    theme = 'hugo-sustain'

El formato de los permalink del tema:

    post = "/:year/:month/:day/:slug" 

Con las siguientes variables se puede añadir la foto del inicio, en la carpeta static del proyecto, debemos crear una carpeta llamada img donde colocaremos una imagen. El creador del tema recomienda que la imagen sea de una dimensión de 190 x 190 pixeles.

    [params]
    avatar = "profile.jpg"
    author = "Jesus Gonzalez" 
    description = "Describe your website"

los iconos de las redes sociales pueden ser mostradas en el inicio. Dentro de las comillas debe colocar los usernames de sus redes sociales.

    [params.social]
    Github        = "username"
    Email         = "email@example.com"
    Twitter       = "username"
    LinkedIn      = "username"
    Stackoverflow = "username"
    Medium        = "username"
    Telegram      = "username"

Con esta variable podemos agregar secciones para navegar a diferentes tópicos del sitio. Para este ejemplo cree una sección blog.

    ## Main Menu
    [[menu.main]]
    name = "blog"
    weight = 100
    identifier = "blog"
    url = "/blog/"

El archivo final debería tener el siguiente formato:

    baseURL = 'http://example.org/'
    languageCode = "en-us"
    title = "gopherblog"
    theme = "hugo-sustain"

    [permalinks]
    post = "/:year/:month/:day/:slug"

    [params]
    avatar = "profile.jpg"
    author = "Jesus Gonzalez"
    description = "tutorial como construir con HUGO"

    [params.social]
    Github        = "username"
    Email         = "email@example.com"
    Twitter       = "username"
    LinkedIn      = "username"
    Stackoverflow = "username"
    Medium        = "username"
    Telegram      = "username"

    ## Main Menu
    [[menu.main]]
    name = "blog"
    weight = 100
    identifier = "blog"
    url = "/blog/"

Es momento de crear el primer post para el blog del proyecto, se puede hacer manualmente pero unas de las ventajas de utilizar HUGO es que con un comando se puede crear los archivos necesarios.

    hugo new blog/primer_post.md

ese comando nos creara los archivos necesarios para crear los posts del blog, estos archivos se anexaran en la carpeta "content". Y el archivo donde podremos agregar nuestro contenido para el post esta en el formato markdown.

Ahora podemos ver en funcionamiento nuestro proyecto ingresando el comando hugo server –D
En algunos tutorial dice que podemos poner en ejecución localmente hugo ingresando el comando:

    hugo serve 

el comando va a funcionar pero los post creados no se van a mostrar porque se encuentran en estado: DRAFT = true, para que el comando nos funcione debemos eliminar la línea del los archivos de post.

    draft: true

si eliminamos esa línea ya podemos ingresar el comando y visualizarlos.

Ahora necesitamos subir nuestro proyecto a un hosting. Para este tutorial utilizare Github Pages.

Para ellos necesitamos crear 2 repositorios

1. Un repositorio con el nombre de tu proyecto Ejemplo

    > hugo_blog

2. Un segundo repositorio con el username de tu cuenta de github

    > username.github.io

    (Recomendación: Este repositorio debe ser creado junto su Readme.md).

3. En la consola git bash que se encuentra abierta en la carpeta de nuestro proyecto agregamos el siguiente comando:

    git remote add origin git@github.com:username/hugo_blog.git

4. Ahora debemos agregar nuestros archivos a la área staging de git eso lo hacemos con los comandos

    git add .
    git commit –m “first commit”

5. Luego debemos subir todo nuestro proyecto a el repositorio del proyecto eso lo hacemos con.

    git push –u origin master

    (Con este accion ya podemos ver en el repositorio de Github todo nuestro proyecto).

6. Hay que clonar el otro repositorio:

    git submodule add -b master git@github.com:username/username.github.io.git public

7. Necesitamos generar la carpeta "public" donde se almacenara los archivos son necesarios para el hosting

    hugo

8. Para finalizar necesitamos crear un Shell script con el nombre de deploy.sh que debe tener lo siguiente:

        #!/bin/sh

        # If a command fails then the deploy stops
        set -e
            
        printf "\033[0;32mDeploying updates to GitHub...\033[0m\n"

        # Build the project.
        hugo -t hugo-sustain # if using a theme, replace with `hugo -t <YOURTHEME>`

        # Go To Public folder
        cd public

        # Add changes to git.
        git add .

        # Commit changes.
        msg="rebuilding site $(date)"
            if [ -n "$*" ]; then
                msg="$*"
            fi
        git commit -m "$msg"

        # Push source and build repos.
        git push origin master

Antes de ejecutar el script debemos cambiar en el archivo config.toml la variable baseURL:

    https://username.github.io/  

ya cambiado esa línea podemos poner en ejecución el script.

    sh deploy.sh

Ahora el sitio puede estar disponible.

<https://username.github.io>

Mi portafolio fue creado con HUGO y el mismo tema:

[Portafolio](https://gonzalezlrjesus.github.io/)
