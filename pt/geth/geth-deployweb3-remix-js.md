# Publicação de smart contract em nó local usando Geth e Remix

Neste tutorial mostrarei passo a passo como compilar um smart contract utilizando Remix e fazer a publicação em um nó local usando Geth.

## Pré-requisitos

- Geth
- Remix - ferramenta web, online

### Geth

Se você não instalou o Geth, veja em 
[Geth install](../../pt/geth/geth-install.md)

### Remix

Vá para
[remix.ethereum.org](http://remix.ethereum.org/)

## Create a Javascript file to deploy a smart contract in Geth console

Primeiro você precisa criar um arquivo Javascript com algumas informações extraídas do Remix.

O tutorial 
[Criando um arquivo Javascript para fazer deploy de um smart contract no console Geth](/pt/remix/remix-create-js-deploy-file.md)
explica esta parte.

## Geth attach ao seu nó

Navegue até a pasta onde está o arquivo `register.js`.
Por exemplo, eu salvei em `C:\ETH\Register` no SO Windows.

```js
cd C:\ETH\Register
```

Execute o comando attach:

```js
geth attach ipc:\\.\pipe\geth.ipc
```

Se você tiver alguma dúvida, saiba mais sobre o [Geth JavaScript Console](/pt/geth/geth-console-attach.md)

## Desbloqueie a conta

```js
personal.unlockAccount(eth.accounts[0], "mypass", 0)
```

## Deploy do smart contract no console Geth

É muito simples, carregamos o script criado com a ABI e Bytecode gerados no Remix,
`register.js`, 
usando o seguinte comando:

```js
loadScript("./register.js");
```

> [!NOTE]
> Perceba que, mesmo se você estiver usando o SO Windows, o caminho do arquivo utiliza `/` ao invés de `\`.

![loadScript](../../images/geth/image-21.png)

Após algumas mensagens, quando a transação do smart contract for incluída em um bloco, você receberá a mensagem "Contract mined!" - contrato minerado.

Normalmente, o prompt de comando da janela desaparecerá após esta mensagem. É só apertar qualquer tecla que ele aparece de novo.

![contract mined!](../../images/geth/image-22.png)

> [!ATTENTION]
> Certifique-se de que está minerando, caso contrário, a mensagem "Contrato minerado!" não aparecerá e o contrato inteligente não será publicado no Blockchain.

## Interagindo com o smart contract

A primeira coisa a fazer é verificar se a instância do smart contract está OK.

Coloque o nome da instância (register), tecle ., e depois pressione a tecla TAB <kbd>&#8677;</kbd> duas vezes para acionar o auto-completar. 
Isto vai apresentar o endereço da publicação, o hash da transação e mais algumas coisas, incluindo todos os métodos disponíveis.

```js
register. [TAB] [TAB]
```

![register . TAB TAB](../../images/geth/image-23.png)

### getInfo

Retorna a string armazenada na variável `info`.

Primeiro verificaremos se existe algum valor armazenado logo após a publicação:

```js
register.getInfo()
```

![register.getInfo](../../images/geth/image-24.png)

Nós não tempos nenhuma informação armazenada, porque não definimos nada no `constructor`, que é a função chamada na publicação do smart contract.

### setInfo

Esta função altera a string armazenada na variável `info`.

Vamos salvar alguma informação no smart contract executando a função:

```js
register.setInfo("Some information", {from:eth.accounts[0]})
```

![register.setInfo](../../images/geth/image-25.png)

Nós recebemos um hash de transação porque enviamos uma transação para alterar o estado do smart contract, que é a mudança do valor da variável info.

### getInfo (again)

Agora que temos a string "Some information" salva, podemos confirmar isto.

Execute a função `getInfo()` de novo:

```js
register.getInfo()
```

![register.getInfo](../../images/geth/image-26.png)

E retornará a info `Some information`.

Agora temos uma informação salva em nosso smart contract, e podemos fazer a leitura da mesma!
:tada: 

:sun_with_face:
