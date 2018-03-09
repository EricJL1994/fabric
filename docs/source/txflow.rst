(ES) Flujo de transacciones
================

`Original <http://hyperledger-fabric.readthedocs.io/en/release/txflow.html>`__ 

Este documento describe las técnicas de transacción durante un intercambio de bienes estandar. El ejemplo incluye dos clientes, A y B, que están comprando y vendiendo rábanos. Cada uno tiene un par en la red mediante el cual pueden enviar sus transaccines e interactuar con el ledger.

.. image:: images/step0.png

**Suposiciones**

Este flujo asume que un canal está configurado y en ejecución. La aplicación de usuario se ha registrado e inscrito con la autoridad de certificados (CA) de la organización y recibido el material criptográfico necesario, que es usado para autenticarse en la red.

El chaincode (que contiene pares valor-clave representando el estado inicial del mercado de rábanos) está instalado en los pares e instanciado en el canal. El chaincode contiene la lógica definiendo las instrucciones de transacción y el precio acordado de los rábanos. También se ha establecido una política de aprobación para este chaincode, estableciendo que tanto ``parA`` como ``parB`` deben ratificar cualquier transacción

.. image:: images/step1.png

1. **El ciente A inicia la transacción**

¿Qué pasa? - El cliente A está enviando una petición para comprar rábanos. La petición se dirige a ``parA`` y ``parB`` ,que son respectivamente representantes del Cliente A y del Cliente B. La política de endose establece que ambos pares deben respaldar cualquier transacción, por lo tanto, la solicitud se envía a ``parA`` y ``parB`` .

A continuación, la propuesta de transacción es construida. Una aplicación basada en un SDK soportado (Node, Java, Python) usa una de las APIs disponibles que genera una propuesta de transacción. La propuesta es una petición para invocar una función del chaincode para que los datos puedan ser leidos y/o escritos en el ledger (por ejemplo, escribir un nuevo par valor-clave de bienes). El SDK sirve como un complemento para empaquetar la propuesta de transacción  en el formato arquitectónico adecuado (búfer de protocolo sobre gRPC) y toma las credenciales criptográficas del usuario para producir una firma única para esta propuesta de transacción.

.. image:: images/step2.png

2. **Los pares que avalan verifican la firma y ejecutan la transacción**

Los pares que respaldan verifican que (1) la propuesta de transacción está bien formada, (2) no se ha enviado ya en el pasado (protección de ataque de repetición), (3) la firma es válida (utilizando MSP) y (4) el remitente (el Cliente A, en el ejemplo) está debidamente autorizado para realizar la operación propuesta en ese canal (es decir, cada par endosante se asegura de que el remitente cumpla con la política de* Escritor *del canal). Los pares endosantes toman las entradas de la propuesta de transacción como argumentos para la función del chaincode invocado. El chaincode se ejecuta luego contra la base de datos de estado actual para producir resultados de transacción que incluyen un valor de respuesta, un conjunto de lectura y un conjunto de escritura. No se realizan actualizaciones en el ledger en este punto. El conjunto de estos valores, junto con la firma del par de endose, se transmite como una "propuesta de respuesta" al SDK que analiza la carga útil de la aplicación que va a consumir.

*{El MSP es un componente de los pares que les permite verificar las solicitudes de transacciones que llegan de los clientes y firmar los resultados de las transacciones (endosos). La política de escritura se define en el momento de creación del canal y determina qué usuario tiene derecho a enviar una transacción a ese canal.}*

.. image:: images/step3.png

3. **Las propuestas de respuesta son inspeccionadas**

La aplicación verifica las firmas de los pares de confirmación y compara las propuestas de respuesta para determinar si las propuestas de respuesta son las mismas. Si el chaincode solo consultaba el ledger, la aplicación inspeccionaría la respuesta de la consulta y normalmente no enviaría la transacción al servicio de pedidos. Si la aplicación del cliente tiene la intención de enviar la transacción al Servicio de pedidos para actualizar el ledger, la aplicación determina si la política de endoso especificada se ha cumplido antes de enviarla (es decir, si tanto parA como parB endosan). La arquitectura es tal que, incluso si una aplicación elige no inspeccionar las respuestas o reenviar una transacción no endosada, la política de endoso seguirá siendo aplicada por los pares y confirmada en la fase de validación de compromiso.

.. image:: images/step4.png

4. **El cliente ensambla la confirmación en una transacción**

La aplicación "difunde" la propuesta de transacción y la respuesta dentro de un "mensaje de transacción" al Servicio de pedido. La transacción contendrá los conjuntos de lectura / escritura, las firmas de los pares endosantes y la identificación del canal. El Servicio de pedidos no necesita inspeccionar todo el contenido de una transacción para realizar su operación, simplemente recibe transacciones de todos los canales en la red, las ordena cronológicamente por canal y crea bloques de transacciones por canal.

.. image:: images/step5.png

5. **La transacción es validada y comprometida**

Los bloques de transacciones se "entregan" a todos los pares en el canal. Las transacciones dentro del bloque se validan para garantizar que se cumpla la política de aprobación y para garantizar que no haya habido cambios en el estado del ledger para las variables de conjunto de lectura dado que el conjunto de lectura fue generado por la ejecución de la transacción. Las transacciones en el bloque se etiquetan como válidas o no válidas.

.. image:: images/step6.png

6. **Ledger actualizado**

Cada par adjunta el bloque a la cadena del canal, y para cada transacción válida, los conjuntos de escritura se envían a la base de datos del estado actual. Se emite un evento para notificar a la aplicación del cliente que la transacción (invocación) se ha anexado de forma inmutable a la cadena, así como para la notificación de si la transacción fue validada o invalidada.

**Note**: See the :ref:`swimlane` diagram to better understand the server side flow and the
protobuffers.

.. Licensed under Creative Commons Attribution 4.0 International License
   https://creativecommons.org/licenses/by/4.0/
