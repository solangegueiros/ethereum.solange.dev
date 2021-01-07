# Create a new project using Truffle

We have two options for initializing a Truffle project:

1. An empty project
2. A project based in a Truffle Box

## 1 - Initialize an empty Truffle project

Create a new folder. For example, `myproject`, and navigate to the folder in the terminal.

```shell
mkdir myproject
cd myproject
```

For example, I will create a folder at this location - `C:\ETH\` (I'm using Windows).

My project can be located in the folder `C:\ETH\myproject`.

![Truffle development console](../../images/truffle/image-08.png)

In your project folder, start an Truffle project by typing the command below into the terminal:

```shell
truffle init
```

![truffle init](../../images/truffle/image-09.png)

Open the folder in VS Code to view the file structure like this:

![truffle file structure](../../images/truffle/image-11.png)

* `./contracts`: All our smart contracts will be stored in this folder.
* `./migrations`: Deployment scripts will be stored in this folder.
* `./test`: Test scripts will be stored in this folder.
* `./truffle-config.js`: This is Truffle's configuration file used to configure networks, including RSK networks.

Note that the following files were also created:

* `Migrations.sol`: Keeps track of which migrations were done on the current network.
* `1_initial_migration.js`: Deployment instructions for `Migrations.sol`.

### Initialize an npm project

When we initialize an empty Truffle project, we also need to initialize an npm project.

Start an npm project in the `myproject` folder by typing the following commands below into the terminal:

```shell
npm init -y
```

![npm init](../../images/truffle/image-12.png)

## 2 - Initialize a project based in a Truffle Box

> [!WARNING]
> Only do this if you have not done option 1.

Truffle Boxes are templates.
In addition to Truffle,
Truffle Boxes can contain other helpful modules, such as Solidity smart contracts, libraries, front-end views, and more.

In option 1, when we use `truffle init`, we used a special kind of truffle box.

To create a project based in a Truffle Box, 
go to [Truffle boxes](en/truffle/truffle-boxes.md) 

:sun_with_face:
