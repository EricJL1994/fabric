(ES) Antes de empezar
===============
`Original <https://hyperledger-fabric.readthedocs.io/en/release-1.0/getting_started.html>`__

Instalar prerequisitos
^^^^^^^^^^^^^^^^^^^^^

Antes de empezar, si no lo ha hecho, es posible que desee comprobar que posee todos los :doc:`prereqs` instalado en la plataforma en la que va a desarrollar las aplicaciones de blockchain y/o operando Hyperledger Fabric.

Instalar Binaries y Docker Images
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Mientras trabajamos en desarrollar instaladores reales para los binarios de Hyperledger Fabric, proporcionamos un script que va a :ref:`binaries` en tu sistema.

Ejemplos de Hyperledger Fabric
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Ofrecemos un conjunto de aplicaciones de ejemplo que, es posible que desee instalar estos :doc:`samples` antes de empezar con los tutoriales ya que aprovechan el código de ejemplo.

Documentación de la API
^^^^^^^^^^^^^^^^^^^^^^^

La documentación para la API Golang de Hyperledger Fabric se puede encontrar en la web de godoc para `Fabric <http://godoc.org/github.com/hyperledger/fabric>`_. Si planea hacer algún desarrollo usando estas APIs, tal vez quiera marcar estos enlaces ahora.

Hyperledger Fabric SDKs
^^^^^^^^^^^^^^^^^^^^^^^

Hyperledger Fabric tiene la intención de ofrecer un numero de SDKs para una amplia variedad de lenguajes de programación. Los dos primeros son los SDKs para Node.js y Java. Esperamos proveer los SDKs para Python y Go después de el lanzamiento de la versión 1.0.0.

  * `Documentación para Hyperledger Fabric Node SDK <https://fabric-sdk-node.github.io/>`__.
  * `Documentación para Hyperledger Fabric Java SDK <https://github.com/hyperledger/fabric-sdk-java>`__.

Hyperledger Fabric CA
^^^^^^^^^^^^^^^^^^^^^

Hyperledger Fabric ofrece un `servicio de autoridad certificadora <http://hyperledger-fabric-ca.readthedocs.io/en/latest>`_ opcional que puede elegir para generar los certificados y claves para configurar y gestionar la identidad en tu red de blockchain. Sin embargo, cualquier CA que pueda generar certificados ECDSA puede ser usado.

Tutoriales
^^^^^^^^^

Ofrecemos 4 tutoriales para empezar con Hyperledger Fabric. El primero está orientado al desarrollador de aplicaciones de Hyperledger Fabric :doc:`write_first_app`. Le lleva a través del proceso de escribir su primera aplicación de blockchain para Hyperledger Fabric usando el `SDK de Node <https://github.com/hyperledger/fabric-sdk-node>`__.

El segundo tutorial está orientado hacia los operadores de red de Hyperledger Fabric, :doc:`build_network`. Este le lleva a través del proceso para establecer una red de blockchain usando Hyperledger Fabric y proporciona una aplicación básica de ejemplo para probarlo.

Finalmente, ofrecemos dos tutoriales de chaincode. Uno orientado a desarrolladores, :doc:`chaincode4ade`, y el otro orientado a operadores, :doc:`chaincode4noah`.

.. note:: Si tiene preguntas no abordadas en esta documentación, o se encuentra con problemas con cualquier tutorial, por favor visite la página :doc:`questions` para más consejos donde puede encontrar ayuda adicional.

.. Licensed under Creative Commons Attribution 4.0 International License
   https://creativecommons.org/licenses/by/4.0/
