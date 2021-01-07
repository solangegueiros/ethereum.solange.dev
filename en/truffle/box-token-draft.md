# Using Truffle Sol token box

Token contracts are most frequently used to exchange or store value.
In this tutorial, I will show you step-by-step how to use the Truffle box [sol-token-box](https://github.com/solangegueiros/sol-token-box), 
which comes with everything you need to create an ERC20 standard token. 
It includes network configuration for deploy on [Görli testnet](https://goerli.net/) network and a mintable ERC20 token.

## Overview

Here is a summary of the steps we will take in this tutorial:

1. [Setup prerequisites](#setup-prerequisites);
2. [Install Sol Token Box](#install-sol-token-box);
3. [Understand the smart contract](#tokensol)
4. [Learn how to use the Truffle development console](#truffle-development-console);
5. [Compile token.sol](#compile-a-smart-contract);
6. [Deploy the smart contract](#deploy-a-smart-contract);
7. [Run tests](#test-a-smart-contract);
8. [Interact with a smart contract in development console](#interact-with-the-token-in-development-console);
9. [Deploy on Goerli testnet](#deploy-on-a-real-blockchain);
10. [Work on Goerli testnet](#rsk-testnet);
11. [Connect to an Goerli network](#connect-to-an-rsk-network);
12. [Test the connection to Goerli network](#test-the-connection-to-rsk-network);
13. [Deploy a smart contract on Goerli network using Truffle](#deploy-the-smart-contract-on-rsk-network);
14. [Interact with the token on Goerli network](#interact-with-the-token-on-rsk-network);
15. [Using the token in a web wallet](#using-the-token-in-a-web-wallet);

If you were redirected from the [Truffle sol-token-box](https://github.com/solangegueiros/sol-token-box) page and successfully executed all the instructions, you can go ahead and interact with the published smart contract:

- [In the Truffle development console](#interact-with-the-token-in-development-console)
- [On Goerli network](#interact-with-the-token-on-goerli-network)
- [Using the token in a web wallet](#using-the-token-in-a-web-wallet)

On the other hand, if you would like to review the steps with more explanatory details and images, you would find this tutorial helpful.

## Setup prerequisites

[truffle-box-prerequisites-content](truffle-box-prerequisites-content.md ':include')

## Install Sol Token Box

The truffle unbox command sets up a project based on a known template. 
In this tutorial, we will be using the "Sol token box" Truffle box, 
which comes with everything you need to create an ERC20 token 
and publish on Görli testnet network.

### Create a new folder

For example, create the folder `my-token`.
Navigate to the folder in the terminal.

```shell
mkdir my-token
cd my-token
```

### Run the unbox command

The truffle unbox command will install all necessary dependencies in the project.

```shell
truffle unbox solangegueiros/sol-token-box
```

This is the result using Windows OS:

![truffle unbox](../../images/rsk-token-box/image-01.png)

### Token.sol

Take a look at the smart contract `Token.sol`. 
You can check it out in folder `contracts`.

```javascript
pragma solidity 0.5.2;
import '@openzeppelin/contracts/token/ERC20/ERC20Mintable.sol';
contract Token is ERC20Mintable{
       string public name = "My token";
       string public symbol = "MTO";
       uint8 public decimals = 2;
}
```

> [!TIP]
> Token.sol has only 7 code lines!

![Token.sol](../../images/rsk-token-box/image-02.png)

This smart contract is a mintable [ERC20](https://eips.ethereum.org/EIPS/eip-20) token. This means that, in addition to the standard ERC20 specification, it has a function for issuing new tokens.

To create our ERC20 Token, we will import `ERC20Mintable` from [Open Zeppelin contracts](https://openzeppelin.com/contracts/). 
This library itself imports several other libraries such as `SafeMath.sol`, the standards for this kind of token, and the capability to mint tokens.

Inside the token, we define some basic information about the token: `name`, `symbol`, and number of `decimals` for the precision.

To inherit the library's attributes and functions, we simply define our contract as a `ERC20Mintable` using the `is` keyword in this way.

## Truffle development console

[truffle-development-console-content](truffle-development-console-content.md ':include')

## Compile a smart contract

In the Truffle console, run this command:

```javascript
compile
```

![truffle compile](../../images/rsk-token-box/image-03.png)

## Deploy a smart contract

[truffle-deploy-content](truffle-deploy-content.md ':include')

Take a look in the file `2_deploy_contracts.js` located in the migrations folder. 

### Migrate

In the Truffle console, run this command:

```javascript
migrate
```

And the `migrate output` should be similar to:

![truffle migrate](../../images/rsk-token-box/image-04.png)

## Test a smart contract

[truffle-test-content](truffle-test-content.md ':include')

Our box also comes with the file `TestToken.js` for testing the smart contract. 
You can check it out in the `test` folder.

Running the tests:

```javascript
test
```

![test](../../images/rsk-token-box/image-05.png)

## Interact with the token in development console

The next commands will run inside the development console.

```shell
truffle develop
```

> [!ATTENTION]
> Make sure you deploy the smart contract before executing this part.

### Get your accounts 

[truffle-console-accounts](truffle-console-accounts.md ':include')

[truffle-console-token](truffle-console-token.md ':include')


### About Token.json

[truffle-artifacts](truffle-artifacts.md ':include')

Networks on Token.json

![json networks](../../images/rsk-token-box/image-08.png)

ABI on Token.json

![json abi](../../images/rsk-token-box/image-09.png)

### Check the total supply

To check if we have tokens already minted, call the `totalSupply` function:

```javascript
(await token.totalSupply()).toString()
```

The returned value is 0, which is expected, since we did not perform any initial mint when we deployed the token.

### Check the token balance

To check the balance of an account, call the `balanceOf` function. For example, to check the balance of account 0:

```javascript
(await token.balanceOf(accounts[0])).toString()
```

Take a look in the results of total supply and balanceOf:

![total supply and balanceOf 0](../../images/rsk-token-box/image-10.png)

The returned value is also 0, which is expected, since we did not make any initial mint when we deployed the token, and by definition no accounts can have any tokens yet.

### Mint tokens

Run this command:

```javascript
token.mint(accounts[0], 10000)
```

This command sent a transaction to mint 100 tokens for account 0. 

![token.mint account 0](../../images/rsk-token-box/image-11.png)

You can also mint to a specific address, `0xa52515946DAABe072f446Cc014a4eaA93fb9Fd79`:

```javascript
token.mint("0xa52515946DAABe072f446Cc014a4eaA93fb9Fd79", 10000)
```

![token.mint address](../../images/rsk-token-box/image-12.png)

### Reconfirm the token balance

Check the balance of account 0 again:

```javascript
(await token.balanceOf(accounts[0])).toString()
```

The returned value is 10000, which is 100 with 2 decimal places of precision. This is exactly what we expected, as we issued 100 tokens

Also, you can get the balance of a specific address, for example, `0xa52515946DAABe072f446Cc014a4eaA93fb9Fd79`:

```javascript
(await token.balanceOf("0xa52515946DAABe072f446Cc014a4eaA93fb9Fd79")).toString()
```

Take a look in the results:

![balanceOf account 0 and address with 10000](../../images/rsk-token-box/image-13.png)

### Check the total supply (again)

Check the total supply again:

```javascript
(await token.totalSupply()).toString()
```

![totalSupply 20000](../../images/rsk-token-box/image-14.png)

The returned value is 20000, which is 200 with 2 decimal places of precision. 
After minting 100 tokens for 2 accounts, this is perfect!

### Transfer tokens

To transfer 40 tokens from account 0 to account 2. 
This can be done by calling the `transfer` function.

```javascript
token.transfer(accounts[2], 4000, {from: accounts[0]})
```

![token.transfer](../../images/rsk-token-box/image-15.png)

Account 2 had no tokens before the transfer, and now it should have 40. Account 1 must have 60 tokens. Also the total supply will be the same.

Let’s check the balance of each account and the total supply:

```javascript
(await token.balanceOf(accounts[2])).toString()
(await token.balanceOf(accounts[0])).toString()
(await token.totalSupply()).toString()
```

Take a look in the results:

![balances after transfer](../../images/rsk-token-box/image-16.png)

Great! The balances of both accounts and the total supply are correct.

### Exit Truffle console

In the Truffle console, enter this command to exit the terminal:

```shell
.exit
```

## Deploy on a real Blockchain

Let's now switch to interacting with a "real" blockchain,
which is running on multiple nodes distributed around the world, across multiple computers!

We need to do some tasks:

- Setup an account / create a wallet
- Update .secret
- Get ETHs
- Connect to a network
- Deploy in the network of your choice

## Create a wallet

The easy way to setup an account is using a web3 wallet injected in the browser.

I present tutorials for some options:
- [Metamask](./en/wallets/metamask.md)

Select the `Görli testnet` network in the web wallet.

![wallets](../../images/rsk-token-box/image-17.png)

Take a look `truffle-config.js` file 

to realize that we are using `HDWalletProvider` ...


## Update .secret file

After create your wallet, update your mnemonic in the file `.secret`, located in the folder project, and save it.

Paste the wallet mnemonic in the file `.secret`, located in the folder project, and save it.

![update mnemonic](../../images/rsk-token-box/image-18.png)

## Get ETHs on Görli testnet

You can get more explanations on how to do it in 
[Görli](/en/wallets/goerli.md) page.

## Connect to Gorli testnet

Run the development console for this network.

```shell
truffle console --network goerli
```

This action instructs Truffle to connect to an Gorli testnet public node and grants it permission to control the accounts created with your mnemonic through the `HD wallet provider`.

## Test the connection to network

[truffle-console-connection](truffle-console-connection.md ':include')

## Deploy on Görli network 

[truffle-migrate-content](truffle-migrate-content.md ':include')

### Running the migrate command 

Run this commands in a terminal (not in Truffle console):

```shell
truffle migrate --network goerli
```

![token migrate RSK testnet](../../images/rsk-token-box/image-20.png)

Congratulations!
:tada:

The token is now published on the network.

> [!ATTENTION]
> Make sure you have enough funds to deploy it. 

Copy the token address. You will use it later.

For example, my token address is [0xDE39436919140C41711c38ba1141117E5B6f26Fe](https://explorer.testnet.rsk.co/address/0xDE39436919140C41711c38ba1141117E5B6f26Fe).

![contract address on RSK Testnet](../../images/rsk-token-box/image-21.png)

## Interact with the token on the network

Interact with the smart contract using Truffle console connected to the network. 
It's the same as we did for Truffle development console, but now it will be for a real blockchain!

> [!ATTENTION]
> Make sure you had deployed the smart contract before executing this part.

Do the same steps which was done before:

- Open Truffle console connected to the network which you deploy the token
- Get your accounts
- Connect with your token
- Check the total supply
- Query the token balance
- Mint tokens
- Transfer tokens

### Truffle console on Gorli testnet

The next commands will run inside the Truffle console, 
connected to the network of your choice. 
In my case, it is testnet:

```shell
truffle console --network testnet
```

### Get your accounts 

[truffle-console-accounts](truffle-console-accounts.md ':include')

[truffle-console-token](truffle-console-token.md ':include')

### Connect with the deployed contract

```javascript
const token = await Token.deployed()
```

### Confirm if the instance is OK.

```javascript
token. [TAB] [TAB]
```

![testnet - token tab tab](../../images/rsk-token-box/image-23.png)

### Check the total supply

To check if we have tokens already minted, call the `totalSupply` function:

```javascript
(await token.totalSupply()).toString()
```

The returned value is 0, which is expected, since we did not perform any initial mint when we deployed the token.

### Check the token balance

To check the balance of an account, call the `balanceOf` function. For example, to check the balance of account 0:

```javascript
(await token.balanceOf(accounts[0])).toString()
```

The returned value is also 0, which is expected, since we did not make any initial mint when we deployed the token, and by definition no accounts can have any tokens yet.

Take a look in the results of total supply and balanceOf:

![testnet - total supply and balanceOf 0](../../images/rsk-token-box/image-24.png)

### Mint tokens

```javascript
token.mint(accounts[0], 10000)
```

This command sent a transaction to mint 100 tokens for account 0. 

![testnet - token.mint account 0](../../images/rsk-token-box/image-25.png)

You can also mint to a specific address, `0xa52515946DAABe072f446Cc014a4eaA93fb9Fd79`:

```javascript
token.mint("0xa52515946DAABe072f446Cc014a4eaA93fb9Fd79", 10000)
```

### Reconfirm the token balance

Check the balance of account 0 again:

```javascript
(await token.balanceOf(accounts[0])).toString()
```

The returned value is 10000, which is 100 with 2 decimal places of precision. This is exactly what we expected, as we issued 100 tokens

Also, you can get the balance of a specific address, for example, `0xa52515946DAABe072f446Cc014a4eaA93fb9Fd79`:

```javascript
(await token.balanceOf("0xa52515946DAABe072f446Cc014a4eaA93fb9Fd79")).toString()
```

### Check the total supply (again)

Check the total supply again:

```javascript
(await token.totalSupply()).toString()
```
The returned value is 20000, which is 200 with 2 decimal places of precision. 
After minting 100 tokens for 2 accounts, this is perfect!

Take a look in the results:

![testnet - balanceOf 2 accounts with 10000 each and totalSupply 20000](../../images/rsk-token-box/image-26.png)

### Transfer tokens

To transfer 40 tokens from account 0 to account 2. 
This can be done by calling the `transfer` function.

```javascript
token.transfer(accounts[2], 4000, {from: accounts[0]})
```

![testnet - token.transfer](../../images/rsk-token-box/image-27.png)

Account 2 had no tokens before the transfer, and now it should have 40. Account 1 must have 60 tokens. Also the total supply will be the same.

Let’s check the balance of each account and the total supply:

```javascript
(await token.balanceOf(accounts[0])).toString()
(await token.balanceOf(accounts[2])).toString()
(await token.balanceOf("0xa52515946DAABe072f446Cc014a4eaA93fb9Fd79")).toString()
(await token.totalSupply()).toString()
```

Take a look in the results:

![testnet - balances after transfer](../../images/rsk-token-box/image-28.png)

Great! The balances of both accounts and the total supply are correct.

### Exit Truffle console

In the Truffle console, enter this command to exit the terminal:

```shell
.exit
```

```windows-command-prompt
truffle(testnet)> .exit

C:\RSK\rsk-token>
```

## Using the token in a web wallet

You can check the balance or send tokens using the previously installed web3 wallet injected in the browser.

### Select the network

Select the same network which you deployed the token, in my case it is `goerli`: 

### Add the token in the wallet

1. Open the tab `tokens`
2. Click the button `Add Token`
3. Go to tab `Custom Token`
4. Paste the token address
5. Click the button `Add`

![Nifty wallet - add custom token](../../images/rsk-token-box/image-29.png)

Great! You can realize that you have 60 tokens, which was the last accounts[0]'s balance after transfer.

![Nifty wallet - token MRT added](../../images/rsk-token-box/image-30.png)

### Create a new account in the web wallet

1. Click the person's icon
2. Choose `Create account`
3. Copy the address of account 2

![Nifty wallet - new account](../../images/rsk-token-box/image-31.png)

It will be created the next account in the web wallet, which must be the same that was listed using Truffle console.

For example, for my mnemonic, account 2 is `0x390Bed29a3f28772eDDcb02750C5a58FE7793647`

> The account's array in Truffle console is zero base indexed, but the web wallet start in account 1. 
> So the account 2 in the web wallet is the accounts[1] in Truffle console.

Repeat the steps to add the token in account 2. 

## Transfer tokens using the web wallet

Select the account 1 again.

Let's transfer 15 tokens from account 1 to account 2.

1. Click the three dots at right side of the token (not in the account 1).
2. Choose send

![Nifty wallet - send token button](../../images/rsk-token-box/image-32.png)

3. Paste the address of account 2, which was copied previously
4. Fill the value: `15.00`
5. Click the button `Next`
6. Click the button `Submit`, to confirm the transaction

![Nifty wallet - send token](../../images/rsk-token-box/image-33.png)

Wait some seconds, when the transaction was mined the balances will change!

![Nifty wallet - balances after transfer](../../images/rsk-token-box/image-36.png)

How about now sending tokens to another account, using the full address? :)

## Final considerations

In this tutorial you learned how to use the Truffle box [sol-token-box](https://github.com/solangegueiros/sol-token-box)
to create your own ERC20 token using Open Zeppelin smart contracts library in Truffle framework, connected to Goerli testnet network.

I hope this tutorial has been helpful and I'd appreciate your feedback. 
Share it if you like it :)

:sun_with_face:
