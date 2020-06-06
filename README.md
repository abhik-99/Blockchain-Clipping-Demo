# Blockchain Clipping Demo

**Authors** - Abhik Banerjee ( [@abhik-99](https://github.com/abhik-99) ) and Sounak Ghosh ( [@maddawck](https://github.com/maddawck/) )

**Language Used** - Python 3.7

The Repo implements Blockchain Clipping for Blockchain Networks between IoT devices. The following are the parts of the network in the proposed concept:-
1. Committing Node.
2. Proposing Node.
3. Certifier / Certifying Authority.
4. Orderer.

### Committing Node
These nodes commit blocks into the blockchain and maintain the blockchain in the network.

### Proposing Node
Proposing nodes can propose new transactions in the network. Incidentally, a proposing node can also be a committing node.

### Certifier / Certifying Authority
Certifier is the entry point in to the network. Certifier provides a signed Digital Certificate (X.509) to the new entrants.

### Orderer
The Orderer is responsible for ordering the blocks. In the current implementation, the role of the orderer is a fixed node. In next revisions, this might also be changed to make an electable orderer.

## How it works.
A new node can ping any existing node to get the address of the Certifier. It has to then provide the certifer with an unsigned Digital Certificate which the CA signs. This acts as the node's identity. The node has to provide this Certificate in all transactions it proposes. All the network nodes know the Public Key of the Certifier and use it to verify the authencity of the Digital Certificate of a node.

Once enrolled, a node can function as a committing node or a proposing node. The Proposed transactions are sent to the Orderer who checks for the validity of the transactions. (This function of the orderer can be changed in the future revisions with the introduction of Endorsing Nodes (similar to Hyperledger Fabric)).

The orderer orders the valid transactions and digital certificates of the proposing node of those transactions into a block and distributes it to the network. This is executed every 2 minutes. This means that for 2 minutes, the orderer waits and collects all the transactions sent its way.

Once a *'LIMIT'* flag is issued by any node in the network ( the node needs to send it to the orderer), the blockchain clipping takes place using the logic discussed in the chapter.

## Start the app.
Fill this space [Sounak](https://github.com/maddawck)

## Project Design. (For [@maddawck](https://github.com/maddawck))
1. Design the orderer node. Put it in **orderer.py**.
2. Design the certifier node. Put it in **ca.py**.
3. Design the committing and proposing node logic. Put it in **blockchain.py**.
4. Design the app as discussed in points 5 and 6. Put it in **app.py**.
5. Host the application using Flask. When starting the app on a "node", the user passess the role of the node in the "--role" along with other arguments.
6. If the "node" is not an Orderer or Certifier, then the user needs to provide their addresses using "--orderer_address" and "--ca_address" flags in the command line along with other arguments.
