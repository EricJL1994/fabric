(ES) Prerequisitos
=============

Instalar cURL
------------

Descargar la última versión de la herramienta `cURL <https://curl.haxx.se/download.html>`__ si no está ya instalada o si tiene errores al ejecutar los comandos de curl de la documentación.

.. note:: Si está utilizando Windows, por favor leer las notas `Extras de Windows`_ debajo.

Docker y Docker Compose
-------------------------

Necesitará instalado lo siguiente en la plataforma en la que se opera o en/para la que se desarrolla.
Hyoerledger Fabric:
  - MacOSX, *nix, o Windows 10: `Docker <https://www.docker.com/products/overview>`__
    Docker versión 17.03.0-ce o superior.
  - Versiones antiguas de Windows: `Docker
    Toolbox <https://docs.docker.com/toolbox/toolbox_install_windows/>`__ -
    , Docker versión Docker 17.03.0-ce o superior.

Puede comprobar la versión de Docker que tiene instalada con el siguiente comando en el terminal:

.. code:: bash

  docker --version

.. note:: Instalar Docker para Mac o Windows, o Docker Toolbox instalará Docker Compose. Si ya tiene Docker instalado, debería comprobar que tiene instalado Docker Compose versión 1.8 o superior. Si no, recomendamos que instale una versión más reciente de Docker.

Puede comprobar la versión de Docker Compose que tiene instalada con el siguiente comando en el terminal:

.. code:: bash

  docker-compose --version

.. _Golang:

Lenguaje de programación Go
-----------------------

Hyperledger Fabric usa el lenguaje de programación Go 1.7.x para algunos de sus componentes.

.. note: Go version 1.8.x will yield test failures

  - `Go <https://golang.org/>`__ - version 1.7.x

Dado que estamos escribiendo un programa de chaincode en Go, necesitamos estar seguros de que el código fuente está situado en algún ligar dentro del arbol ``$GOPATH``. Primero, necesita comprobar que la variable del entorno ``$GOPAHT`` está definida.

.. code:: bash

  echo $GOPATH
  /Users/xxx/go

Si no se muestra nada con echo ``$GOPATH``, necesitará configurarlo. Normalmente, el valor será un subdirectorio de tu espacio de desarrollo si tiene uno, o uno de tu directorio $HOME. Como vamos a hacer mucha programación en Go, es poasible que desee agregar lo siguiente a tu ``~/.bashrc``:

.. code:: bash

  export GOPATH=$HOME/go
  export PATH=$PATH:$GOPATH/bin

Node.js Runtime y NPM
-----------------------

Si va a desarrollar aplicaciones para Hyperledger Fabric aprovechando el Hyperledger Fabric SDK para Node.js, necesitará tener instalada la versión 6.9.x de Node.js

.. note:: La versión 7.x de Node.js no es compatible en este momento.

  - `Node.js <https://nodejs.org/en/download/>`__ - version 6.9.x o superior

.. note:: Instalar Node.js también instalará NPM, sin embargo es recomendado confirmar la versión NPM instalada. Puede actualizar la herramienta ``npm`` con el siguiente comando:

.. code:: bash

  npm install npm@3.10.10 -g

Extras de Windows
--------------

Si está desarrollando en Windows, querrá trabajar dentro de Docker Quickstart Terminal, que proporciona una mejor alternativa al incorporado en Windows como `Git Bash <https://git-scm.com/downloads>`__ que normalmente obtienes como parte de la instalación de Docker Toolbox en Windows 7.

Si embargo, la experiencia demuestra que es un entorno de desarrollo pobre con funcionalidades limitadas. Es adecuado para ejecutar casos basados en Docker, tales como :doc:`getting_started`, pero puede tener dificultades con operaciones que involucren el comando ``make``.

Antes de ejecutar ningún comando ``git clone``, ejecuta los siguientes comandos:

::

    git config --global core.autocrlf false
    git config --global core.longpaths true

Puedes comprobar los ajustes de estos parámetros con los siguientes comandos:

::

    git config --get core.autocrlf
    git config --get core.longpaths

Necesitan estar en ``false`` y ``true`` respectivamente.

El comando ``curl`` que viene con Git y Docker Toolbox es antiguo y no soporta correctamente la redirección usada en :doc:`getting_started`. Asegurese de instalar y usar una nueva versión desde la `página de descargas cURL <https://curl.haxx.se/download.html>`__

Para Node.js también necesita las herramientas de Visual Studio C++ Build Tools necesarias, que están disponible de forma gratuita y pueden ser instalada con el siguiente comando:

.. code:: bash

	  npm install --global windows-build-tools

Mirar la página `NPM windows-build-tools <https://www.npmjs.com/package/windows-build-tools>`__ para más detalles.

Una vez que esto esté hecho, debería installar el módulo NPM GRPC con el siguiente comando:

.. code:: bash

	  npm install --global grpc

Su entorno debería estar listo para realizar los ejemplos y tutoriales de :doc:`getting_started`.

.. note:: Si tiene preguntas no abordadas en esta documentación, o se encuentra con problemas con cualquier tutorial, por favor visite la página :doc:`questions` para más consejos donde puede encontrar ayuda adicional.

.. Licensed under Creative Commons Attribution 4.0 International License
   https://creativecommons.org/licenses/by/4.0/
