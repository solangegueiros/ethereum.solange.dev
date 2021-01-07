
No Truffle console,
você pode verificar o saldo da `accounts[0]` antes de fazer o deploy de um smart contract, 
para ter certeza de que tem fundos suficientes. 

Guarde as contas na variável `accounts`:

```javascript
const accounts = await web3.eth.getAccounts()
```

Consulte o saldo:

```javascript
(await web3.eth.getBalance(accounts[0])).toString()
```

![getBalance](../../images/truffle/image-12.png)
