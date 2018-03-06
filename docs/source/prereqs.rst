Prerequisitos
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

Node.js Runtime and NPM
-----------------------

If you will be developing applications for Hyperledger Fabric leveraging the
Hyperledger Fabric SDK for Node.js, you will need to have version 6.9.x of Node.js
installed.

.. note:: Node.js version 7.x is not supported at this time.

  - `Node.js <https://nodejs.org/en/download/>`__ - version 6.9.x or greater

.. note:: Installing Node.js will also install NPM, however it is recommended
          that you confirm the version of NPM installed. You can upgrade
          the ``npm`` tool with the following command:

.. code:: bash

  npm install npm@3.10.10 -g

Extras de Windows
--------------

If you are developing on Windows, you will want to work within the
Docker Quickstart Terminal which provides a better alternative to the
built-in Windows such as `Git Bash <https://git-scm.com/downloads>`__
which you typically get as part of installing Docker Toolbox on
Windows 7.

However experience has shown this to be a poor development environment
with limited functionality. It is suitable to run Docker based
scenarios, such as :doc:`getting_started`, but you may have
difficulties with operations involving the ``make`` command.

Before running any ``git clone`` commands, run the following commands:

::

    git config --global core.autocrlf false
    git config --global core.longpaths true

You can check the setting of these parameters with the following commands:

::

    git config --get core.autocrlf
    git config --get core.longpaths

These need to be ``false`` and ``true`` respectively.

The ``curl`` command that comes with Git and Docker Toolbox is old and
does not handle properly the redirect used in
:doc:`getting_started`. Make sure you install and use a newer version
from the `cURL downloads page <https://curl.haxx.se/download.html>`__

For Node.js you also need the necessary Visual Studio C++ Build Tools
which are freely available and can be installed with the following
command:

.. code:: bash

	  npm install --global windows-build-tools

See the `NPM windows-build-tools page
<https://www.npmjs.com/package/windows-build-tools>`__ for more
details.

Once this is done, you should also install the NPM GRPC module with the
following command:

.. code:: bash

	  npm install --global grpc

Your environment should now be ready to go through the
:doc:`getting_started` samples and tutorials.

.. note:: If you have questions not addressed by this documentation, or run into
          issues with any of the tutorials, please visit the :doc:`questions`
          page for some tips on where to find additional help.

.. Licensed under Creative Commons Attribution 4.0 International License
   https://creativecommons.org/licenses/by/4.0/
