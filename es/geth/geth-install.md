# Instalando Geth

Hay varias formas de instalar Geth:

- usando un administrador de paquetes - package manager;
- descarga de un paquete preconstruido independiente;
- funcionando como contenedor docker;
- construyéndolo usted mismo.

<!-- tabs:start -->

#### ** Linux **

### Instalando Geth en Linux

Ingresa los siguientes comandos en bash para instalar Geth:

```shell
mkdir -p ~/code/ethereum/geth-node
cd ~/code/ethereum/geth-node
curl \
  -L \
  https://gethstore.blob.core.windows.net/builds/geth-darwin-amd64-1.9.24-cc05b050.tar.gz
  > geth-darwin-amd64-1.9.24-cc05b050.tar.gz

tar -xf geth-darwin-amd64-1.9.24-cc05b050.tar.gz

cd geth-darwin-amd64-1.9.24-cc05b050

ls -l

./geth version
```

Linux tiene muchas versiones diferentes, así ve a la
[official install Geth page](https://geth.ethereum.org/docs/install-and-build/installing-geth)
para encontrar más opciones para instalar Geth.

#### ** Mac OS **

### Instalando Geth en Mac OS

La forma más sencilla de hacerlo es con [Homebrew](https://brew.sh/).

Si no lo tiene, instale `Homebrew` ejecutando este comando en la terminal:

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

Y luego instale `Geth`:

```shell
brew tap ethereum/ethereum
brew install ethereum
```

#### ** Windows OS **

[geth-install-windows](geth-install-windows.md ':include')

<!-- tabs:end -->

> [!NOTE]
> Este tutorial se realizó usando la versión 1.9.24, recomiendo usarla.

## Geth version

En la terminal, ejecuta este comando para verificar la versión, si se ejecuta y devuelve una versión, esto significa que `geth` se instaló correctamente:

```shell
geth version
```

![geth version](../../images/geth/image-28.png)

## Geth help

La ayuda de la línea de comandos es muy útil:

```shell
geth --help
```

![geth help](../../images/geth/image-29.png)

## Ejecutando Geth

> [!ATTENTION]
> Por defecto, Geth ejecuta un nodo de la red principal.
> Esto significa que ejecutando `geth` en la terminal,
> se comenzará a descargar toda la base de datos para la red principal de Ethereum!
> 
> Si tu objetivo es usar Geth en una red específica, no ejecutes `geth` sin ningún parámetro.

Navega a lo siguiente tutorial antes de esta acción.

[Geth - crea un nodo local](/es/geth/geth-local-node.md)

:sun_with_face:

## Reference links

- [Official install Geth page](https://geth.ethereum.org/docs/install-and-build/installing-geth)

- [Geth documentation](https://geth.ethereum.org/docs/)

- [Archived Geth documentation](https://github.com/ethereum/go-ethereum/wiki)

- [List of stable releases](https://github.com/ethereum/go-ethereum/releases)

