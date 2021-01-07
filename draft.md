:sun_with_face:

# TO DO

[] imagens em geth-install-windows.md


### Remix Images

D:\BLOCKCHAIN\SOLANGE.DEV\GITHUB\solange.dev\content\blog\2020\blockopoly-01\images

### Installing Geth on Windows OS

Images: 
https://docs.google.com/document/d/1okLV4o6M_0z0rzFBfcI5AT7j--nEdAA3ETYy_gZ5iP4/edit#

![Geth download page](/assets/img/tutorials/geth-attach-local-node/image-04.png)

![Geth install](/assets/img/tutorials/geth-attach-local-node/image-05.png)



# Geth - create a local node

## Overview

We will do these steps:

1. [Download and install Geth](#download-and-install-geth);
2. [Create a genesis file](#genesis-file);
3. [Inicialize a new Blockchain](#geth-init);
4. [Running Geth](#running-geth);
5. [IPC path](#ipc-path);
6. [Connect to Geth node using IPC](#attaching-a-javascript-console-to-you-node);

## Overview ES

Haremos estos pasos:

1. [Descarga e instalación de Geth](#descarga-e-instalación-de-geth);
2. [Crea un archivo de génesis](#archivo-de-génesis);
3. [Inicializa un nuevo Blockchain](#geth-init);
4. [Ejecutando Geth](#ejecutando-geth);
5. [Ruta de IPC](#ruta-de-ipc);
6. [Conéctase al nodo Geth usando IPC](#conéctase-al-nodo-geth-usando-ipc);

## Overview PT

Executaremos estas etapas:

1. [Download and instalação do Geth](#download-and-install-geth);
2. [Crie um arquivo genesis](#genesis-file);
3. [Inicialize um novo Blockchain](#geth-init);
4. [Executando Geth](#running-geth);
5. [IPC path](#ipc-path);
6. [Conexão ao nó Geth usando IPC](#attaching-a-javascript-console-to-you-node);

# Geth JavaScript Console

## Overview

We will do these steps:

1. [Run a Geth local node](#run-a-geth-local-node)
2. [Connect to Geth with IPC - Geth attach](#geth-attach-using-ipc);
3. [Personal and Accounts](#personal-and-accounts);
4. [Mining](#mining);
5. [Balances](#balances);
6. [Unlock an account](#unlock-an-account);
7. [Transfer funds between accounts](#transfer-ethers);

## Overview ES

Realizaremos estos pasos:

1. [Ejecutando el nodo Geth](#ejecutando-el-nodo-geth)
2. [Conectando a Geth con IPC](#geth-attach-con-ipc);
3. [Personal y Accounts](#personal-y-accounts);
4. [Mineria](#mining);
5. [Saldos](#saldos);
6. [Unlock an account](#unlock-an-account);
7. [Transfer funds between accounts](#transfer-ethers);

## Overview PT

Faremos estas etapas:

1. [Executando o nó local Geth](#run-a-geth-local-node)
2. [Connect to Geth with IPC - Geth attach](#geth-attach-usando-ipc);
3. [Personal e Accounts](#personal-e-accounts);
4. [Mineração](#mineração);
5. [Saldos](#saldos);
6. [Unlock an account](#unlock-an-account);
7. [Transfer funds between accounts](#transfer-ethers);

# Deploy a smart contract at local node using Geth and Remix

## Overview

We will do these steps:

1. Run a Geth local node;
2. Connect with a local node using Geth attach;
3. Create a smart contract in Remix;
4. Compile it;
5. Create a Javascript deploy file;
6. Deploy the smart contract in the Geth console;
7. Interact with the smart contract.


# Create a Javascript file to deploy a smart contract in Geth console

[remix-create-register](remix-create-register.md ':include')

[remix-compile-register](remix-compile-register.md ':include')


