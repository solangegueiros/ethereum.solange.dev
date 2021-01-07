---
title: Blockopoly - parte 2
date: "2020-06-29T13:00:00.000Z"
description: "Na parte 2 do tutorial Blockopoly você vai criar mais um smart contract da arquitetura do jogo, o gerenciador de ativos 'AssetManager' e interagir com ele, entendendo sua lógica e funcionamento no Blockchain."
tags: tutorial, ethereum, rsk, smart-contract, reactors
type: blog
---

Neste tutorial você vai aprender passo por passo como criar o jogo Blockopoly uma divertida variação de um famoso jogo de tabuleiro. A ideia principal do jogo mapeia muito bem os sistemas Blockchain e vamos construir partes do jogo para demonstrar isto.

Nosso jogo é composto por 3 smart contracts: 
- Bank
- AssetManager
- Blockopoly

Na [parte 1](/2020/blockopoly-01/) apresentamos a arquitetura do jogo e criamos o primeiro smart contract: `Bank`, que controla o dinheiro, os saldos de cada um, a emissão e transferências.  

Nesta segunda parte do tutorial continuaremos com o gerenciador de ativos, o smart contract `AssetManager`, que é o administrador das propriedades que serão negociadas. 

# Asset Manager

`AssetManager` é um gerenciador de ativos, no nosso caso é o administrador das propriedades que serão negociadas. 

As propriedades do nosso jogo serão os espaços [Microsoft Reactors](https://developer.microsoft.com/en-us/reactor/) espalhados pelo mundo:

![Microsoft Reactors](/images/image-39.png)

* Redmond Reactor
* Seattle Reactor
* San Francisco Reactor
* New York Reactor
* Toronto Reactor
* London Reactor
* Sao Paulo Reactor
* Tel Aviv Reactor
* Stockholm Reactor
* Abu Dhabi Reactor
* Sydney Reactor
* Shanghai Reactor
* Bangalore Reactor

Nestes espaços profissionais da área se encontram, aprendem e se conectam - tanto aos colegas locais quanto às idéias e tecnologias líderes da indústria na Microsoft, parceiros e comunidades de código aberto.

## Crie o smart contract

Clique no 2o botão do lado esquerdo - `file explorers`.

Clique no símbolo `+` create a new file.

Nome do arquivo / file name: `AssetManager.sol`

![filename assetManager.sol](/images/image-40.png)

Copie o códido fonte:

```javascript
pragma solidity >=0.5.0 <0.7.0;
 
contract AssetManager {
    address public manager;
 
    struct Asset {
        address owner;
        string name;
        uint price;
        bool exists;
    }
 
    mapping (uint => Asset) private assets;
 
    event AssetAdded(address sender, string name);
    event AssetTransfered(address sender, address from, address to, string name);

    constructor() public {
        manager = msg.sender;
    }
 
    function addAsset(string memory _name, uint _price, address  _owner) public {
        require(msg.sender == manager, "Only the Asset Manager can add assets");
        uint assetId = uint(keccak256(abi.encodePacked(_name)));
        require(!assets[assetId].exists, "Asset name already added");
 
        Asset memory a = Asset({
            owner: _owner,
            name: _name,
            price: _price,
            exists: true
          }
        ); 
        assets[assetId] = a;

        emit AssetAdded(msg.sender, _name);
    }
 
    function getOwner(string memory _name) public view returns (address) {
        uint assetId = uint(keccak256(abi.encodePacked(_name)));
        Asset memory a = assets[assetId];
        require(a.exists, "Asset does not exist");
        return a.owner;
    }
 
    function transferAsset(address from, address to, string memory _name) public {
        require(msg.sender == manager, "Only the AssetManager can transfer assets");
        uint assetId = uint(keccak256(abi.encodePacked(_name)));
        Asset memory a = assets[assetId];
 
        require(a.exists, "Asset must exist");
        require(a.owner == from, "Asset must be owned by from address");
 
        a.owner = to;
        assets[assetId] = a;
 
        emit AssetTransfered(msg.sender, from, to, _name);
    }
}
```

E cole aqui:

![Remix AssetManager.sol](/images/image-41.png)

## AssetManager.sol

Este smart contract contém:

### Variáveis

* Uma variável pública `manager` para saber qual o endereço do administrador de ativos.
* Uma estrutura chamada `Asset`, que armazena todas as informações de um ativo: proprietário, nome do ativo, preço e se ele existe.
* Um mapping chamado `assets`, privado, que armazena um identificador associando-o a uma estrutura com as informações de um ativo.

### Eventos

* Um evento `AssetAdded` que avisa quando algum ativo for adicionado no jogo.
* Um evento `AssetTransfer` que avisa quando algum ativo for transferido de um endereço a outro no jogo.

### Construtor

O `constructor` (construtor), executado apenas no momento da criação do smart contract, define quem é o `manager`.

### Funções

* Uma função `addAsset` que adiciona os ativos no jogo.
* Uma função `getOwner` que retorna quem é o proprietário de um ativo.
* Uma função `transferAsset` para transferir um ativo de uma pessoa para outra.

## Compile o smart contract

Como a opção auto-compile está habilitado, provavelmente você verá o sinal verde no 3o botão com a mensagem `compilation successful`.

Caso isto não aconteça, compile manualmente:

* Clique no 3o botão do lado esquerdo - Solidity compiler
* Clique no botão `Compile AssetManager.sol`

![Compile AssetManager.sol](/images/image-42.png)

Verifique o sinal verde no 3o botão com a mensagem `compilation successful`

![compilation successful](/images/image-43.png)

## Publique o smart contract localmente

No painel à esquerda, clique no botão `Deploy and run transactions`. Atualmente é o 4o botão.

Confira se o smart contract `AssetManager` está selecionado na lista.

![select contract](/images/image-44.png)

Clique no botão `Deploy`.

![deploy](/images/image-45.png)

Confira na parte de baixo, à direita, a mensagem: `creation of  AssetManager pending …` e, em seguida, a transação de criação do smart contract.

![transaction](/images/image-46.png)

Se quiser ver os detalhes da transação, clique na seta à direita do botão Debug. 

## Interagindo com o smart contract

Quando fazemos a publicação de um smart contract utilizando Remix, podemos encontrá-lo no painel a esquerda, no item deploy and run transactions, `Deployed Contracts`:

Veja na parte debaixo da tela se o smart contract foi publicado:

![Deployed Contracts](/images/image-47.png)

Clique em `>`:

![AssetManager expand](/images/image-48.png)

Aparecerão as mesmas funções que criamos em nosso smart contract!

![AssetManager ABI](/images/image-49.png)

### Manager

Clique no botão `manager` e veja quem é o gerente no smart contract. É a conta que fez a publicação do smart contract. Em nosso caso, a primeira conta da lista `ACCOUNT`, final  `0C8B1`.

![manager](/images/image-50.png)

Veja a chamada da função no terminal, embaixo, à direita: 

![manager transaction](/images/image-51.png)

Você pode acompanhar detalhes como custo de gás e conta para todas as chamadas de funções pelo terminal.

### Adicionar propriedade

Vamos chamar a função `addAsset` com os seguintes parâmetros:

* nome: `Redmond Reactor`
* preço: `100`
* dono: o endereço: `0xFF2a31390E9Bb3dcD947b03f133248bA9840ff6B`

> Clique na seta para baixo, no lado direito do botão `addAsset`, para expandir os parâmetros.

![addAsset parameters](/images/image-52.png)

Após preencher os parâmetros, clique no botão `transact`.

Veja os detalhes da transação no terminal:

![addAsset transact](/images/image-53.png)

### Evento *AssetAdded*

Expanda os detalhes da transação `addAsset` e procure a parte logs. Você encontrará o evento `AssetAdded`, com os detalhes da inclusão da propriedade:

* Sender - quem cadastrou

* Name - nome da propriedade

![event AssetAdded](/images/image-54.png)

### Dono de uma propriedade

Para saber quem é o dono de uma propriedade, utilize a função `getOwner`. 

Por exemplo, vamos verificar a propriedade cadastrada anteriormente.  Preencha o parâmetro: `Redmond Reactor` e clique no botão `getOwner`:

![getOwner](/images/image-55.png)

O resultado é o endereço da conta cadastrada anteriormente.

### Transferir propriedade

Utilize a função `transferAsset` para transferir uma propriedade. Expanda a função e veja as informações a serem enviadas:

* From: o dono atual
* To: o novo dono, para quem vai transferir
* Name: nome da propriedade

Por exemplo, vamos transferir a propriedade cadastrada anteriormente para a conta `0xb3718630A94e39ba85933a669F2b531697918F0a`.  Preencha os parâmetros:

* From: `0xFF2a31390E9Bb3dcD947b03f133248bA9840ff6B`
* To: `0xb3718630A94e39ba85933a669F2b531697918F0a`
* Name: `Redmond Reactor`

Clique no botão `transact`

![transact transferAsset](/images/image-56.png)

### Evento *AssetTransfered*

Expanda os detalhes da transação `transferAsset` e procure a parte `logs`. Você encontrará o evento `AssetTransfered`, com os detalhes da transferência da propriedade:

* Sender - quem enviou a transação
* From - dono anterior
* To - novo dono
* Name - nome da propriedade

Veja nosso exemplo:

![event AssetTransfered](/images/image-57.png)

## Propriedades disponíveis

Não foi implementada uma função para listar as propriedades disponíveis. Você pode pensar como implementá-la :)

# Próximos passos

Nesta parte do tutorial do jogo `Blockopoly` foi ensinado como criar o smart contract `AssetManager` utilizando a linguagem Solidity. Ele é nosso gerenciador de ativos, ou seja, o administrador das propriedades negociadas. 

Na [parte 1](/2020/blockopoly-01/) você conheceu a arquitetura do projeto e o primeiro smart contract: `Bank`, que controla o dinheiro, os saldos de cada um, a emissão e transferências.

Lembre-se que nosso jogo é composto de 3 smart contracts: 

* Bank
* AssetManager
* Blockopoly

Na última parte do tutorial construiremos o "coração" do projeto, que é o smart contract `Blockopoly`. Nele são definidos jogadores, propriedades negociadas, início, final do jogo e o ganhador. Além disto, demonstraremos o funcionamento de uma partida.

Continue em [Blockopoly - parte 3](/2020/blockopoly-03/).

Espero que esse tutorial tenha sido útil e agradeço caso tenha algum feedback para mim. Compartilhe o artigo caso tenha gostado :)

> Aguarde um vídeo sobre o assunto em meu canal: <a href="https://www.youtube.com/user/solangegueiros" target="_blank"> youtube Solange Gueiros</a>. Se quiser ser avisado quando a publicação acontecer é só assinar o canal.
