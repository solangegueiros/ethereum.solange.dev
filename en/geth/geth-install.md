# Installing Geth

There are several ways to install Geth:

- using a package manager;
- downloading a standalone pre-built bundle; 
- running as a docker container; 
- building it yourself. 

<!-- tabs:start -->

#### ** Linux **

### Installing Geth on Linux OS

Enter the commands below on bash to install Geth:

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

Linux has many different versions, so check it out the 
[official install Geth page](https://geth.ethereum.org/docs/install-and-build/installing-geth)
to find more options to install Geth.

#### ** Mac OS **

### Installing Geth on Mac OS

The easiest way to is using [Homebrew](https://brew.sh/).

If you don’t have it, install `Homebrew` running this command in the terminal:

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

And then install `Geth`:

```shell
brew tap ethereum/ethereum
brew install ethereum
```

#### ** Windows OS **

[geth-install-windows](geth-install-windows.md ':include')

<!-- tabs:end -->

> [!NOTE]
> This tutorial was made using version 1.9.24, I recommend to use this version.

## Geth version

In the terminal, run this command to check the version, if it runs and returns a version, this means `geth` was installed successfully:

```shell
geth version
```

![geth version](../../images/geth/image-28.png)

## Geth help

The command line help is very useful:

```shell
geth --help
```

![geth help](../../images/geth/image-29.png)

## Running Geth

> [!ATTENTION]
> By default, Geth runs a mainnet node. 
> It will starts to download the entire database for Ethereum mainnet! 
> 
> If your goal is to use Geth on a specific network, don't run `geth` without any parameters. 

Navigate into the next tutorial before this action.

[Geth - create a local node](/en/geth/geth-local-node.md)

:sun_with_face:

## Reference links

- [Official install Geth page](https://geth.ethereum.org/docs/install-and-build/installing-geth)

- [Geth documentation](https://geth.ethereum.org/docs/)

- [Archived Geth documentation](https://github.com/ethereum/go-ethereum/wiki)

- [List of stable releases](https://github.com/ethereum/go-ethereum/releases)

