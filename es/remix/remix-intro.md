# Remix

Remix es una herramienta web online. 
Es un IDE (Integrated Development Environment = Entorno de Desarrollo Integrado) que se utiliza para escribir, compilar, implementar y depurar código Solidity. 
Puede conectarse a una billetera web, como Metamask y, a través de esta conexión, usarse para implementar contratos inteligentes en diferentes redes.

Se puede acceder en:
[remix.ethereum.org](http://remix.ethereum.org/)

![Remix](../../images/remix/image-01.png)

## Environment Solidity

En la página de inicio - home / welcome page, elija environment `Solidity`

![Remix environment Solidity](../../images/remix/image-02.png)

## Terminal

En Remix, en la parte de abajo, a la derecha, hay una terminal con algunas bibliotecas disponibles.

Puedes enviar comandos y transacciones aquí. 
Esta área también presenta el resultado de transacciones y / o llamadas a funciones de contrato inteligente.

![remix terminal](../../images/remix/image-03.png)

> [!NOTE]
> ¡Esta zona de retorno es muy importante para mirar los resultados!

## Compilador Solidity

En el tercer botón en el lado izquierdo, haz clic en Solidity compiler

![remix solidity compiler](../../images/remix/image-04.png)

Es útil habilitar la compilación automática (auto-compile), para compilar contratos inteligentes automáticamente al editar en Remix.

![auto-compile](../../images/remix/image-05.png)

## Deploy and run transactions

En Remix, en el lado izquierdo, ubica el botón `Deploy and run transactions` (Implementar y ejecutar transacciones).
Por ahora es el cuarto botón

![deploy and run transactions](../../images/remix/image-06.png)

Remix tiene el entorno de desarrollo `JavaScriptVM`, un simulador de Blockchain que tiene lugar en la memoria del navegador.

![JavaScriptVM](../../images/remix/image-07.png)

## Accounts

Este simulador tiene varias direcciones / cuentas con Ethers ficticios que podemos elegir para publicar un contrato inteligente o interactuar con él.

A continuación, se muestra un ejemplo de una lista de cuentas:

![account](../../images/remix/image-08.png)

Cada vez que inicie Remix o actualice la página, la lista de cuentas puede cambiar.

## Smart contracts

Los contratos inteligentes se encuentran en el segundo botón a la izquierda: `file explorers`

![file explorers](../../images/remix/image-09.png)
