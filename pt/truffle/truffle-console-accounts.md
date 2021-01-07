
Obtenha suas contas no Truffle console

No Truffle console, digite:

```javascript
const accounts = await web3.eth.getAccounts()
```

> [!TIP]
> Não se preocupe com o retorno `undefined`, é normal. 

Veja a lista de contas digitando o comanbo abaixo:

```javascript
accounts
```

Para ver a primeira conta:

```javascript
accounts[0]
```

E a segunda conta:

```javascript
accounts[1]
```

Ve o resultado das contas:

![accounts](../../images/truffle/image-07.png)


### Saldos

Para consultar o saldo de uma conta, por exemplo, `accounts[0]`,
execute este comando no Truffle console:

```javascript
(await web3.eth.getBalance(accounts[0])).toString()
```

O resultado retornado está em `wei`:

![getBalance](../../images/truffle/image-12.png)
