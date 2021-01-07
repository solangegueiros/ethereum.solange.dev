
Obtenga sus cuentas en la consola Truffle.

En la consola Truffle, ingrese:


```javascript
const accounts = await web3.eth.getAccounts()
```

> [!TIP]
> No se preocupe por la devolución `undefined`, es el defecto.

Ves la lista de direcciones ingresando el siguiente comando:

```javascript
accounts
```

Para ver la primera cuenta:

```javascript
accounts[0]
```

Y la segunda cuenta:

```javascript
accounts[1]
```

Echa un vistazo a las cuentas:

![accounts](../../images/truffle/image-07.png)


### Saldos

Para consultar el saldo de una cuenta, 

To check the balance of an account, por ejemplo, `accounts[0]`,
ejecute este comando en la consola Truffle:

```javascript
(await web3.eth.getBalance(accounts[0])).toString()
```

El resultado se devuelve en `wei`:

![getBalance](../../images/truffle/image-12.png)
