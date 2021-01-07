
### Faça a conexão com seu token

Em primeiro lugar, faça a conexão ao token:

```javascript
const token = await Token.deployed()
```

Agora a variável `token` contém a instância do token publicado anteriormente.

![token deployed](../../images/truffle-sol-token-box/image-09.png)

> [!TIP]
> Não se preocupe com o retorno `undefined`, é normal. 

### Verifique se a instância está OK

Escreva o nome da variável:  `token`, tecle `.` e depois aperte a tecla <kbd>&#8677;</kbd> TAB duas vezes para acionar o recurso autocompletar. 
Será apresentado o endereço e hash da transação na publicação, além de outras coisas, incluindo todas as váriaveis e métodos públicos disponíveis. 

```javascript
token. [TAB] [TAB]
```

![token tab tab](../../images/truffle-sol-token-box/image-10.png)


### Consulte o total de tokens

Chame a função `totalSupply` para verificar a quantidade de tokens já emitidos:

```javascript
(await token.totalSupply()).toString()
```

O valor retornado é 0, o que é esperado, dado que nós não fizemos uma emissão inicial ao publicar o token.

### Consulte o saldo de tokens

Chame a função `balanceOf` para saber o saldo de uma conta, por exemplo, da conta 0:

```javascript
(await token.balanceOf(accounts[0])).toString()
```

O valor retornado é 0, o que também é esperado, como não foi realizada uma emissão inicial ao publicar o token, o saldo de todas as contas será 0.

Veja os resultados para total supply e balanceOf:

![total supply and balanceOf 0](../../images/truffle-sol-token-box/image-13.png)

### Emitindo tokens

Execute este comando:

```javascript
token.mint(accounts[0], 10000)
```

Está sendo enviada uma transação para a emissão de 100,00 tokens para a conta 0. 

![token.mint account 0](../../images/truffle-sol-token-box/image-14.png)

Também é possível emitir para um endereço específico, por exemplo: `0xa52515946DAABe072f446Cc014a4eaA93fb9Fd79`:

```javascript
token.mint("0xa52515946DAABe072f446Cc014a4eaA93fb9Fd79", 10000)
```

![token.mint address](../../images/truffle-sol-token-box/image-15.png)

### Consultando o saldo de tokens (de novo)

Verifique o saldo da conta 0 novamente:

```javascript
(await token.balanceOf(accounts[0])).toString()
```

O valor retornado é 10000, o que significa 100 com 2 casas decimais de precisão.
Isto é exatamente o que esperávamos, dado que emitimos 100 tokens

Você também pode consultar o saldo de um endereço específico, por exemplo, `0xa52515946DAABe072f446Cc014a4eaA93fb9Fd79`:

```javascript
(await token.balanceOf("0xa52515946DAABe072f446Cc014a4eaA93fb9Fd79")).toString()
```

Veja os saldos:

![balanceOf account 0 and address with 10000](../../images/truffle-sol-token-box/image-18.png)

### Consultando o total supply (de novo)

Verifique o total de tokens novamente:

```javascript
(await token.totalSupply()).toString()
```

![totalSupply 20000](../../images/truffle-sol-token-box/image-19.png)

O valor retornado é 30000, que são 300 tokens com 2 casas decimais de precisão.
Depois de emitir 100 tokens para cada uma das 3 contas, está correto!

### Transfira tokens

Eu gostaria de transferir 40,00 tokens da primeira conta (`accounts[0]`) para a terceira conta (`accounts[2]`). 
Farei isto chamando a função `transfer`.

```javascript
token.transfer(accounts[2], 4000, {from: accounts[0]})
```

![token.transfer](../../images/truffle-sol-token-box/image-20.png)

**O que acontece depois da transferência?**

- accounts[2] não tinha tokens antes, e agora deveria ter 40. 
- accounts[0] terá 60 tokens agora. 
- o total supply (emissão total) deve permanecer a mesma.

Vamos consultar o saldo de cada conta e a emissão total

- Saldo de accounts[2]:

```javascript
(await token.balanceOf(accounts[2])).toString()
```

- Saldo de accounts[0]:

```javascript
(await token.balanceOf(accounts[0])).toString()
```

- Total supply mais uma vez:

```javascript
(await token.totalSupply()).toString()
```

Veja os resultados:

![balances after transfer](../../images/truffle-sol-token-box/image-21.png)

Maravilha!
Os saldos das duas contas e a emissão total estão corretos.

