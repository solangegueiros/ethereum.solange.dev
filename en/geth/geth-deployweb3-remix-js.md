# Deploy a smart contract at local node using Geth and Remix

In this tutorial I will show you step-by-step how to compile a smart contract using Remix and deploy it on a local node using Geth.

## Requirements

- Geth
- Remix - web tool, online

### Geth

If you don't have Geth installed, 
go to [Geth install](/en/geth/geth-install.md)

### Remix

Go to 
[remix.ethereum.org](http://remix.ethereum.org/)

## Create a Javascript file to deploy a smart contract in Geth console

First you need to create a Javascript file with some information extracted from Remix.

The tutorial 
[Create a Javascript file to deploy a smart contract in Geth console](/en/remix/remix-create-js-deploy-file.md)
explains this part.

## Geth attach to your node

Go to the folder where is located the `register.js` file. 
For example, I saved it in `C:\ETH\Register` in Windows OS.

```shell
cd C:\ETH\Register
```

Run the attach command:

```shell
geth attach ipc:\\.\pipe\geth.ipc
```

If you have any doubt, learn more about the [Geth JavaScript Console](/en/geth/geth-console-attach.md).

## Unlock account

```js
personal.unlockAccount(eth.accounts[0], "mypass", 0)
```

## Deploy the smart contract at Geth console

This is quite simple, load the script created with the ABI and Bytecode generated in Remix, 
`register.js`, 
using the following command:

```js
loadScript("./register.js");
```

> [!NOTE]
> Even if you are using Windows OS, the file path should use `/` instead of `\`.

![loadScript](../../images/geth/image-21.png)

As soon as the smart contract is validated and included in a block, you'll receive the message "Contract mined!".

Usually, the command prompt disappears after the return message. You may press any key to show it again.

![contract mined!](../../images/geth/image-22.png)

> [!ATTENTION]
> Be sure you are mining, otherwise the message "Contract mined!" will not appear and the smart contract will not be published on the Blockchain.

## Interact with the smart contract

The first thing to do is check if our deployed instance is OK.

Type the instance's name (register), hit `.`, then hit TAB <kbd>&#8677;</kbd> twice to trigger autocomplete. 
This will display the published address, transaction hash of deploy, among other things, including all methods available.

```js
register. [TAB] [TAB]
```

![register . TAB TAB](../../images/geth/image-23.png)

### getInfo

It returns the string stored at variable `info`.

You can check if we have some info at smart contract:

```js
register.getInfo()
```

![register.getInfo](../../images/geth/image-24.png)

We don't nothing stored, because we didn't define anything in the constructor, which is the function called when a smart contract is deployed.

### setInfo

It is a function to update the string stored at variable `info`.

Let's save some information in the smart contract by invoking it:

```js
register.setInfo("Some information", {from:eth.accounts[0]})
```

![register.setInfo](../../images/geth/image-25.png)

We got a transaction hash because we sent a transaction to change the state of a smart contract, which update the variable `info`.

### getInfo (again)

We have the string "Some information" saved, and we can check it.

Run the function `getInfo()` again:

```js
register.getInfo()
```

![register.getInfo](../../images/geth/image-26.png)

And it returned the info `Some information`.

Now we have stored information in our smart contract, and are able to retrieve it!
:tada:

:sun_with_face:
