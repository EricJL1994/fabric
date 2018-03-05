Transaction Flow
================

This document outlines the transactional mechanics that take place during a standard asset
exchange.  The scenario includes two clients, A and B, who are buying and selling
radishes.  They each have a peer on the network through which they send their
transactions and interact with the ledger.



*Este documento describe las técnicas de transacción durante un intercambio de bienes estandar. El ejemplo incluye dos clientes, A y B, que están comprando y vendiendo rábanos. Cada uno tiene un par en la red mediante el cual pueden enviar sus transaccines e interactuar con el ledger.*

.. image:: images/step0.png

**Assumptions**

This flow assumes that a channel is set up and running.  The application user
has registered and enrolled with the organization’s certificate authority (CA)
and received back necessary cryptographic material, which is used to authenticate
to the network.

The chaincode (containing a set of key value pairs representing the initial
state of the radish market) is installed on the peers and instantiated on the
channel.  The chaincode contains logic defining a set of transaction
instructions and the agreed upon price for a radish. An endorsement policy has
also been set for this chaincode, stating that both ``peerA`` and ``peerB`` must endorse
any transaction.



*Este flujo asume que un canal está configurado y en ejecución. La aplicación de usuario se ha registrado e inscrito con la autoridad de certificados (CA) de la organización y recibido el material criptográfico necesario, que es usado para autenticarse en la red.*

*El chaincode (que contiene pares valor-clave representando el estado inicial del mercado de rábanos) está instalado en los pares e instanciado en el canal. El chaincode contiene la lógica definiendo las instrucciones de transacción y el precio acordado de los rábanos. También se ha establecido una política de aprobación para este chaincode, estableciendo que tanto* ``parA`` *como* ``parB`` *deben ratificar cualquier transacción*

.. image:: images/step1.png

1. **Client A initiates a transaction**

What's happening? - Client A is sending a request to purchase radishes.  The
request targets ``peerA`` and ``peerB``, who are respectively representative of
Client A and Client B. The endorsement policy states that both peers must endorse
any transaction, therefore the request goes to ``peerA`` and ``peerB``.

Next, the transaction proposal is constructed.  An application leveraging a supported
SDK (Node, Java, Python) utilizes one of the available API's which generates a
transaction proposal.  The proposal is a request to invoke a chaincode function
so that data can be read and/or written to the ledger (i.e. write new key value
pairs for the assets).  The SDK serves as a shim to package the transaction proposal
into the properly architected format (protocol buffer over gRPC) and takes the user’s
cryptographic credentials to produce a unique signature for this transaction proposal.



1. **El ciente A inicia la transacción**

*¿Qué pasa? - El cliente A está enviando una petición para comprar rábanos. La petición se dirige a* ``parA`` *y* ``parB`` *,que son respectivamente representantes del Cliente A y del Cliente B. La política de endose establece que ambos pares deben respaldar cualquier transacción, por lo tanto, la solicitud se envía a* ``parA`` *y* ``parB``*.*

*A continuación, la propuesta de transacción es construida. Una aplicación basada en un SDK soportado (Node, Java, Python) usa una de las APIs disponibles que genera una propuesta de transacción. La propuesta es una petición para invocar una función del chaincode para que los datos puedan ser leidos y/o escritos en el ledger (por ejemplo, escribir un nuevo par valor-clave de bienes). El SDK sirve como un complemento para empaquetar la propuesta de transacción  en el formato arquitectónico adecuado (búfer de protocolo sobre gRPC) y toma las credenciales criptográficas del usuario para producir una firma única para esta propuesta de transacción.*

.. image:: images/step2.png

2. **Endorsing peers verify signature & execute the transaction**

The endorsing peers verify (1) that the transaction proposal is well formed,
(2) it has not been submitted already in the past (replay-attack protection),
(3) the signature is valid (using MSP), and (4) that the
submitter (Client A, in the example) is properly authorized to perform
the proposed operation on that channel (namely, each endorsing peer ensures that
the submitter satisfies the channel's *Writers* policy).
The endorsing peers take the transaction proposal inputs as
arguments to the invoked chaincode's function. The chaincode is then
executed against the current state database to produce transaction
results including a response value, read set, and write set.  No updates are
made to the ledger at this point. The set of these values, along with the
endorsing peer’s signature is passed back as a “proposal response” to the SDK
which parses the payload for the application to consume.

{The MSP is a peer component that allows them to verify
transaction requests arriving from clients and to sign transaction results(endorsements).
The Writing policy is defined at channel creation time, and determines
which user is entitled to submit a transaction to that channel.}



2. **Los pares que avalan verifican la firma y ejecutan la transacción**

*Los pares que respaldan verifican que (1) la propuesta de transacción está bien formada, (2) no se ha enviado ya en el pasado (protección de ataque de repetición), (3) la firma es válida (utilizando MSP) y (4) el remitente (el Cliente A, en el ejemplo) está debidamente autorizado para realizar la operación propuesta en ese canal (es decir, cada par endosante se asegura de que el remitente cumpla con la política de* Escritor *del canal). Los pares endosantes toman las entradas de la propuesta de transacción como argumentos para la función del chaincode invocado. El chaincode se ejecuta luego contra la base de datos de estado actual para producir resultados de transacción que incluyen un valor de respuesta, un conjunto de lectura y un conjunto de escritura. No se realizan actualizaciones en el ledger en este punto. El conjunto de estos valores, junto con la firma del par de endose, se transmite como una "propuesta de respuesta" al SDK que analiza la carga útil de la aplicación que va a consumir.*

.. image:: images/step3.png

3. **Proposal responses are inspected**

The application verifies the endorsing peer signatures and compares the proposal
responses to determine if the proposal responses are the same. If the chaincode only queried
the ledger, the application would inspect the query response and would typically not
submit the transaction to Ordering Service. If the client application intends to submit the
transaction to Ordering Service to update the ledger, the application determines if the specified
endorsement policy has been fulfilled before submitting (i.e. did peerA and peerB both endorse).
The architecture is such that even if an application chooses not to inspect responses or otherwise
forwards an unendorsed transaction, the endorsement policy will still be enforced by peers
and upheld at the commit validation phase.

.. image:: images/step4.png

4. **Client assembles endorsements into a transaction**

The application “broadcasts” the transaction proposal and response within a
“transaction message” to the Ordering Service. The transaction will contain the
read/write sets, the endorsing peers signatures and the Channel ID.  The
Ordering Service does not need to inspect the entire content of a transaction in order to perform
its operation, it simply receives
transactions from all channels in the network, orders them chronologically by
channel, and creates blocks of transactions per channel.

.. image:: images/step5.png

5. **Transaction is validated and committed**

The blocks of transactions are “delivered” to all peers on the channel.  The
transactions within the block are validated to ensure endorsement policy is
fulfilled and to ensure that there have been no changes to ledger state for read
set variables since the read set was generated by the transaction execution.
Transactions in the block are tagged as being valid or invalid.

.. image:: images/step6.png

6. **Ledger updated**

Each peer appends the block to the channel’s chain, and for each valid transaction
the write sets are committed to current state database. An event is emitted, to
notify the client application that the transaction (invocation) has been
immutably appended to the chain, as well as notification of whether the
transaction was validated or invalidated.

**Note**: See the :ref:`swimlane` diagram to better understand the server side flow and the
protobuffers.

.. Licensed under Creative Commons Attribution 4.0 International License
   https://creativecommons.org/licenses/by/4.0/
