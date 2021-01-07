
En la consola Truffle
puede verificar el saldo de la `accounts[0]` antes de implementar el contrato inteligente,
para asegurarse de tener fondos suficientes.

Guarde las cuentas en la variable `accounts`:

```javascript
const accounts = await web3.eth.getAccounts()
```

Consulta el saldo:

```javascript
(await web3.eth.getBalance(accounts[0])).toString()
```

![getBalance](../../images/truffle/image-12.png)
