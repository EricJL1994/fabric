Antes de empezar
===============

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

Hyperledger Fabric provides an optional
`certificate authority service <http://hyperledger-fabric-ca.readthedocs.io/en/latest>`_
that you may choose to use to generate the certificates and key material
to configure and manage identity in your blockchain network. However, any CA
that can generate ECDSA certificates may be used.

Tutorials
^^^^^^^^^

We offer four initial tutorials to get you started with Hyperledger Fabric.
The first is oriented to the Hyperledger Fabric **application developer**,
:doc:`write_first_app`. It takes you through the process of writing your first
blockchain application for Hyperledger Fabric using the Hyperledger Fabric
`Node SDK <https://github.com/hyperledger/fabric-sdk-node>`__.

The second tutorial is oriented towards the Hyperledger Fabric network
operators, :doc:`build_network`. This one walks you through the process of
establishing a blockchain network using Hyperledger Fabric and provides
a basic sample application to test it out.

Finally, we offer two chaincode tutorials. One oriented to developers,
:doc:`chaincode4ade`, and the other oriented to operators,
:doc:`chaincode4noah`.

.. note:: If you have questions not addressed by this documentation, or run into
          issues with any of the tutorials, please visit the :doc:`questions`
          page for some tips on where to find additional help.

.. Licensed under Creative Commons Attribution 4.0 International License
   https://creativecommons.org/licenses/by/4.0/
