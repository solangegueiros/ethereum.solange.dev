
In the Truffle console,
you can check the balance of `accounts[0]` before deploy the smart contract, 
to be sure that you have enough funds. 

Retrieve the accounts:

```javascript
const accounts = await web3.eth.getAccounts()
```

Get balance:

```javascript
(await web3.eth.getBalance(accounts[0])).toString()
```

![getBalance](../../images/truffle/image-12.png)
