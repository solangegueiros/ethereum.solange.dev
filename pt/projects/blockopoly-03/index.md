---
title: Blockopoly - parte 3
date: "2020-06-29T12:00:00.000Z"
description: "Nesta terceira e última parte deste projeto Blockchain desenvolveremos o smart contract `Blockopoly` e demonstraremos o funcionamento de uma partida."
tags: tutorial, ethereum, rsk, smart-contract, reactors
type: blog
---

Neste tutorial você vai aprender passo por passo como criar o jogo Blockopoly, uma divertida variação de um famoso jogo de tabuleiro. A ideia principal do jogo mapeia muito bem os sistemas Blockchain e vamos construir partes do jogo para demonstrar isto.

Nosso jogo é composto por 3 smart contracts: 
- Bank
- AssetManager
- Blockopoly

Na [parte 1](/2020/blockopoly-01/) apresentamos a arquitetura do jogo e criamos o primeiro smart contract: `Bank`, que controla o dinheiro, os saldos de cada um, a emissão e transferências.  

Na [parte 2](/2020/blockopoly-02/) foi ensinado como criar o smart contract `AssetManager`, nosso gerenciador de ativos, que é o administrador das propriedades negociadas. 

Nesta terceira e última parte construiremos o smart contract `Blockopoly` e demonstraremos o funcionamento de uma partida.

# Blockopoly

O `Blockopoly` é smart contract principal do jogo. Através dele são definidos os jogadores, as propriedades negociadas, o início e final do jogo.

![Monopoly - Ylanite Koppens - Pexels](/images/image-58.png)

Imagem: [Ylanite Koppens - Pexels](https://www.pexels.com/pt-br/foto/abstrato-banco-imobiliario-borrao-brincadeiras-776654/)

Escolha quem vai ser o banqueiro. 
Esse jogador é responsável por todo o dinheiro e pelas propriedades que ainda pertencem ao banco. 
O banqueiro vai publicar o smart contract `Blockopoly`.

## Crie o smart contract

Clique no 2o botão do lado esquerdo - `file explorers`.

Clique no símbolo `+` create a new file.

Nome do arquivo / file name: `Blockopoly.sol`

![filename Blockopoly.sol](/images/image-59.png)

Copie o códido fonte:

```javascript
pragma solidity >=0.5.0 <0.7.0;
 
import "./Bank.sol";
import "./AssetManager.sol";
 
contract Blockopoly {
    address public banker;
    Bank public bank;
    AssetManager public assetManager;

    struct  Player {
        address addr;
        string name;
    }
    Player[] public players;
    mapping(string => bool) public names;
    mapping(address => Player) public addrPlayerMapping;

    bool public started;
    uint256 private endTime;
 
    event GameStarted();
    event PlayerJoined(address player, string name);

    constructor() public {
        banker = msg.sender;
        bank = new Bank();
        bank.mint(banker, 100000);
        
        assetManager = new AssetManager();
        publishProperties();
    }
 
    function publishProperties() private {
        assetManager.addAsset("Redmond Reactor", 100, banker);
        assetManager.addAsset("Seattle Reactor", 100, banker);
        assetManager.addAsset("San Francisco Reactor", 100, banker);
        assetManager.addAsset("New York Reactor", 100, banker);
        assetManager.addAsset("Toronto Reactor", 100, banker);
        assetManager.addAsset("London Reactor", 100, banker);
        assetManager.addAsset("Sao Paulo Reactor", 100, banker);
        assetManager.addAsset("Tel Aviv Reactor", 100, banker);
        assetManager.addAsset("Stockholm Reactor", 100, banker);
        assetManager.addAsset("Abu Dhabi Reactor", 100, banker);
        assetManager.addAsset("Sydney Reactor", 100, banker);
        assetManager.addAsset("Shanghai Reactor", 100, banker);
        assetManager.addAsset("Bangalore Reactor", 100, banker);
    }
 
    function startGame() public {
        require(msg.sender == banker, "Only the Banker can start the game");
        require(!started, "Game already started");
 
        uint length = players.length;
        require(length >= 2, "Need at least two players");
 
        for(uint i = 0; i < length; i++) {
            Player memory p = players[i];
            bank.mint(p.addr, 1000);
        }
 
        started = true;
        endTime = now + 15 minutes;
        emit GameStarted();
    }

    function joinGame(string memory _name) public {
        require(players.length < 6, "Game is full");
        require(!names[_name], "Name is already taken");
 
        Player memory p = Player({
            addr: msg.sender,
            name: _name
          }
        );
        players.push(p);
        names[_name] = true;
        addrPlayerMapping[msg.sender] = p;
 
        emit PlayerJoined(msg.sender, _name);
    }
 
    function buyProperty(string memory _name) public {
        require(started, "Game not started");
        require(now <= endTime, "Game over");

        address owner = assetManager.getOwner(_name);
        uint price = 100;
 
        require(owner != msg.sender, "Player can't already own the property");
        require(bank.getBalance(msg.sender) >= price, "Insuficcient funds");
 
        bank.sendMoney(owner, msg.sender, price);
        assetManager.transferAsset(owner, msg.sender, _name);
    }
    
    function getWinner() public view returns (string memory winner) {
        require(started, "Game not started");
        require(now > endTime, "Game not ended");

        uint winnerIndex;
        uint greaterBalance = 0;
        uint auxBalance = 0;
        
        for (uint i = 0; i <  players.length; i++) {
            auxBalance = bank.getBalance(players[i].addr);
            if (auxBalance > greaterBalance) {
                winnerIndex = i;
                greaterBalance = auxBalance;
            }
        }
        return players[winnerIndex].name;
    }    
}
```

E cole no arquivo `Blockopoly.sol`.

![Remix Blockopoly.sol](/images/image-60.png)

## Blockopoly.sol

Blockopoly.sol importa os outros smart contracts criados anteriormente:

```javascript
import "./Bank.sol";
import "./AssetManager.sol";
```

Este smart contract é o mais complexo de todos, entenda cada parte:

### Variáveis

* Uma variável pública `banker` que define quem é o banqueiro do jogo;
* Uma variável pública `bank`, que é o smart contract banco, importado;
* Uma variável pública `assetManager`, que é o smart contract gerenciador de ativos, também importado;
* Uma estrutura chamada `Player`, que armazena todas as informações de um jogador: endereço (account) e nome;
* Um array `players` que é  a lista pública de jogadores;
* Um mapping chamado `names`, público, que controla se um nome já está sendo utilizado no jogo;
* Um mapping chamado `addrPlayerMapping`, público, que faz a associação entre o endereço / conta de uma pessoa e o jogador que ela está utilizando;
* Uma variável pública `started` que define se a partida começou;
* Uma variável pública `endTime` que define quando a partida termina;

### Eventos

* Um evento `GameStarted` que avisa quando o jogo começou;
* Um evento `PlayerJoined` que avisa quando um jogador entrou no jogo;

### Construtor

O `constructor` (construtor) é executado apenas no momento da criação do jogo.  Ele executa as seguintes tarefas:
* define quem é o banqueiro
* cria o banco
* faz a emissão inicial de moedas da partida
* cria o gerenciador de ativos
* chama a função que cria as propriedades disponíveis na partida.

### Funções

* A função `publishProperties` cria as propriedades disponíveis na partida. Esta função é privada, então só pode ser chamada por um smart contract. Ela é invocada pelo construtor;
* A função `startGame` inicia o jogo;
* A função `joinGame` possibilita que uma pessoa entre na partida;
* A função `buyProperty` é para alguém comprar uma propriedade;
* `getWinner` informa quem é o vencedor da partida.

## Compile o smart contract

Como a opção auto-compile está habilitado, provavelmente você verá o sinal verde no 3o botão com a mensagem `compilation successful`.

Caso isto não aconteça, compile manualmente:

* Clique no 3o botão do lado esquerdo - Solidity compiler
* Clique no botão `Compile Blockopoly.sol`

> Nosso projeto precisa do compilador na versão 0.5.5 ou acima.

![Compile Blockopoly.sol](/images/image-61.png)

Verifique o sinal verde no 3o botão com a mensagem `compilation successful`.

![compilation successful](/images/image-62.png)

## Publique o smart contract localmente

No painel à esquerda, clique no botão `Deploy and run transactions`. Atualmente é o 4o botão.

### Gas Limit

Gas Limit é a máxima quantidade de gás que permitimos gastar na publicação do smart contract.

O smart contract `Blockopoly` é maior e mais complexo do que os anteriores, e por este motivo é preciso aumentar o `Gas Limit`.

* Aumente o `Gas Limit` para `6000000` (seis milhões).

![Gas Limit](/images/image-63.png)

### Limpe a lista de contratos

Se você fez a parte 1 e 2 deste tutorial, utilizando uma das contas da lista do Remix, já publicamos os smart contracts `Bank` e `AssetManager`. 
Porém eles serão publicados novamente pelo smart contract `Blockopoly`.
Para evitar confusão, é melhor limpar a lista `Deployed Contracts`, que apresenta os smart contracts já publicados anteriormente.

Clique no ícone da lixeira, localizado ao lado direito de `Deployed Contracts`.

![Clean Deployed Contracts](/images/image-64.png)

E a lista aparecerá vazia novamente:

![Deployed Contracts list empty](/images/image-65.png)

### Selecione o contrato

O arquivo `Blockopoly.sol` importa outros dois smart contracts (`Bank` e `AssetManager`), então os três aparecerão na lista `Contract`. 

> É fundamental selecionar o smart contract `Blockopoly`!

![select contract](/images/image-66.png)

### Deploy

Clique no botão `Deploy`.

![deploy](/images/image-67.png)

No terminal, abaixo e à direita, aparecerá a mensagem: `creation of  Blockopoly pending …` e, em seguida, a transação da criação do smart contract.

![transaction](/images/image-68.png)

Se quiser ver os detalhes da transação, clique na seta à direita do botão Debug. 

## Interagindo com o smart contract

Veja o smart contract publicado no painel à esquerda, no item deploy and run transactions, `Deployed Contracts`:

![Deployed Contracts](/images/image-69.png)

Clique em `>`:

![Blockopoly expand](/images/image-70.png)

Aparecerão as mesmas funções que criamos em nosso smart contract!

![Blockopoly ABI](/images/image-71.png)

# Vamos jogar!

O objetivo do jogo é se tornar o jogador mais rico através da compra e venda de propriedades.

## Regras do jogo

Estas são as regras do jogo:

1. O banqueiro publica o jogo
2. Os jogadores entram
3. Inicia a partida
4. Os jogadores alternam sua vez para jogar
5. Na sua vez, o jogador escolhe uma propriedade e compra
6. O final do jogo acontece depois de 15 minutos
7. Quem tiver mais dinheiro no final do jogo ganha
8. Se dois jogadores possuírem o mesmo saldo, o critério de desempate é quem se cadastrou primeiro na partida.

## Publicação do jogo

O banqueiro vai publicar o jogo, ou seja, o smart contract `Blockopoly`.
Esse jogador é responsável por todo o dinheiro e pelas propriedades que ainda pertencem ao banco. 

Por exemplo, eu fiz a publicação a partir da conta 1, final `5ED40`. 
Esta conta é o banqueiro.
Você pode conferir quem é o banqueiro chamando a função `banker`, clicando no botão equivalente:

![banker](/images/image-72.png)

Veja a chamada da função: 

![transaction](/images/image-73.png)

> O banqueiro não pode ser um jogador "normal", quem for o banqueiro fará exclusivamente este papel.

## Entrada dos jogadores

Cada pessoa que desejar participar do jogo deve chamar a função `joinGame`, informando seu nome.

### Primeiro Jogador: Ana

Na lista Account, selecione a segunda conta. Na minha lista é a conta final  `Bd037`.

Então a conta 2 será o primeiro jogador e seu nome será `Ana`.

![select account](/images/image-74.png)


Para chamar a função `joinGame`, vou informar o parâmetro `Ana` e clicar no botão `joinGame`. 

![joinGame](/images/image-75.png)

A conta 2 é registrada como jogador, com o nome associado.

### Evento *PlayerJoined*

Veja os detalhes da transação:

![event PlayerJoined](/images/image-76.png)

Expanda a transação e procure a parte logs. Você encontrará o evento `PlayerJoined`, com os detalhes do jogador.

![imageAltText](/images/image-77.png)

### Variável *addrPlayerMapping*

Outra forma de conferir os dados da jogadora `Ana`, é fazendo uma chamada para o visualizador da variável `addrPlayerMapping`, passando a conta 2 como parâmetro.  

Veja o resultado:

![addrPlayerMapping](/images/image-78.png)

### Segundo Jogador: Ben

Na lista Account, selecione a terceira conta. Na minha lista é a conta final  `0EE5c`.

![select account](/images/image-79.png)

Execute novamente a função `joinGame`, agora com o parâmetro `Ben`.

![joinGame](/images/image-80.png)

Veja o log da transação:

![event PlayerJoined](/images/image-81.png)

Ou consulte o mapping:

![addrPlayerMapping](/images/image-82.png)

## Início do jogo

Quando todos os participantes já tiverem entrado, o banqueiro inicia o jogo chamando a função `startGame`.

> Neste momento cada jogador recebe 1000 moedas para jogar.

Em nosso jogo, as pessoas jogarão alternadamente, começando na ordem em que se inscreveram através da função `joinGame`. 

Isto é um acordo verbal, mas pode ser implementado no smart contract futuramente.

Então vamos lá! Vá para a conta 1, que é o banqueiro, e clique no botão `startGame`. 

![startGame](/images/image-83.png)

Você enviou uma transação para o smart contract:

 ![transact startGame](/images/image-84.png)

### Evento *GameStarted*

Expanda a transação e procure a parte logs. Você encontrará o evento `GameStarted`, que avisa ao mundo que o jogo começou!

![GameStarted](/images/image-85.png)

### Variável *Started*

Consulte se o jogo foi iniciado, chamando o visualizador da variável started:

![Started](/images/image-86.png)

Ele retorna `True`, ou seja, jogo inciado.

> A partir de agora o jogo vai durar 15 minutos!

## Saldos dos jogadores

O smart contract `Bank` é quem controla os saldos dos jogadores.

### Instância do *Bank*

Para verificar um saldo, é preciso instanciar o smart contract `Bank` que foi publicado pelo smart contract `Blockopoly`.

Isto é realizado em 2 passos:

1. Descubra o endereço da publicação realizada para este smart contract
2. Selecione o smart contract na lista `CONTRACT`
3. Clique em `At Address` passado como parâmetro o endereço descoberto

Vamos detalhar cada passo:

1. Para descobrir o endereço do smart contract `Bank`, clique no botão `Bank`:

![Bank address](/images/image-87.png)

O retorno será o endereço do smart contract `Bank` publicado pelo smart contract `Blockopoly`.

No meu exemplo: `0x5f15a500767Fdb21aDF61d98099799Eb4DCd95fA`

2. Vá na lista `CONTRACT` e selecione o smart contract `Bank`:

![Bank select](/images/image-88.png)

3. Preencha o endereço no campo ao lado do botão  `At Address` e clique no botão:

![Bank address](/images/image-89.png)

Veja na lista de contratos a instância do `Bank`:

![Bank instance](/images/image-90.png)

Clique em `>` para ver as funções do `Bank`.

### getBalance

* Escolha o endereço na lista `ACCOUNT`.
* Preencha o endereço no parâmetro ao lado do botão `getBalance` e clique no botão.

No caso, quero saber o saldo das contas 2 e 3, que são os jogadores Ana e Ben.

Saldo da conta 2, da Ana:

![Ana account](/images/image-91.png)

![Ana balance](/images/image-92.png)

Saldo da conta 3, do Ben:

![Ben account](/images/image-93.png)

![Ben balance](/images/image-94.png)

> Isto foi detalhado no smart contract `Bank`, criado na [parte 1](/2020/blockopoly-01/) deste tutorial.

## Propriedades disponíveis

O smart contract `AssetManager` é quem gerencia as propriedades disponíveis.

Não foi implementada uma função para listar as propriedades disponíveis. Este controle será realizado fora do Blockchain, faz parte da estratégia do jogo, por enquanto.

### Instância do *AssetManager*

É preciso instanciar o smart contract `AssetManager` que foi publicado pelo smart contract `Blockopoly`, da mesma forma que fizemos com o contrato `Bank`.

1. Para descobrir o endereço do smart contract `AssetManager`, clique no botão `AssetManager` do contrato `Blockopoly` :

![AssetManager address](/images/image-95.png)

No meu exemplo: `0x66CaD295B47aD7dbe091Fd18f334b6D7871d9794`

2. Vá na lista `CONTRACT` e selecione o smart contract `AssetManager`:

![AssetManager select](/images/image-96.png)

3. Preencha o endereço no campo ao lado do botão  `At Address` e clique no botão:

![AssetManager address](/images/image-97.png)

Veja na lista de contratos a instância do `AssetManager`:

![AssetManager instance](/images/image-98.png)

Clique em `>` para ver as funções do `AssetManager`.

### Dono de uma propriedade

Para saber quem é o dono de uma propriedade, utilize a função `getOwner`. Preencha o parâmetro nome da propriedade.

Por exemplo, veremos o proprietário de `Sao Paulo Reactor`:

![getOwner Sao Paulo Reactor](/images/image-99.png)

É a conta 1, do banqueiro.

No início do jogo, ele é o proprietário de todas as propriedades. Veja mais um, `Redmond Reactor`:

![getOwner Redmond Reactor](/images/image-100.png)

> Isto foi explicado no smart contract `AssetManager`, criado na [parte 2](/2020/blockopoly-02/) deste tutorial. 

# Comprando uma propriedade

Alternadamente, cada jogador vai comprar uma propriedade.
Ao chegar a sua vez, o jogador vai escolher a propriedade que deseja comprar. 

Utilize a função `buyProperty` para comprar uma propriedade.

### Ana comprará "Sao Paulo Reactor"

![buyProperty Sao Paulo Reactor](/images/image-101.png)

Veja o log da transação: 

![transaction buyProperty](/images/image-102.png)

### Eventos

Esta transação emite 2 eventos: 

* `Sent` - o envio de moedas para a compra
* `AssetTransfered` - a transferência da propriedade de um endereço para outro

![buyProperty events](/images/image-103.png)

### Continuando as compras 

Ben comprará "Redmond Reactor".

Depois Ana escolherá outra propriedade para comprar, e assim sucessivamente, até acabar o tempo.

### Algumas dicas

* Faz parte do jogo cada um ter seu controle de propriedades ainda disponíveis.
* Se um jogador tentar comprar uma propriedade que já é sua, ele terá desperdiçado a sua vez.
* Melhor comprar as propriedades do banco primeiro!
* Quando um jogador compra uma propriedade de outro jogador ao invés de comprar do banco, ele está pagando para outro jogador, ou seja, está aumentando o saldo do outro, então esta não é a melhor estratégia.
* A qualquer momento você pode consultar uma propriedade para saber quem é o seu dono.
* Você não pode consultar o saldo de outra pessoa.

# Término do jogo

Foi definido no smart contract `Blockopoly` que o jogo encerra 15 minutos após seu início.
E quem tiver mais dinheiro no final do jogo ganha.

Os jogadores vão alternando a sua vez. Em algum momento, quando o jogador tentar comprar uma propriedade, não vai conseguir e receberá a mensagem `Game over`.

Isto pode ser acompanhado na tentativa de execução da transação:

![Revert Game over](/images/image-104.png)

# Ganhador

Após receber a mensagem `Game over`, chame a função `getWinner` para descobrir o ganhador da partida.

**Ana ganhou!**

![getWinner](/images/image-105.png)

> Se dois jogadores possuírem o mesmo saldo, o critério de desempate é quem se cadastrou primeiro na partida.

# Próximos passos - upgrades

Existem diversas melhorias que podem ser implementadas nos smart contracts do jogo `Blockopoly`.

Aqui estão algumas sugestões:

## Cadastro múltiplo

Atualmente a mesma conta / endereço pode se cadastrar 2x, isto não é correto. Como você pode corrigir isto?

## Propriedades disponíveis

Não foi implementada uma função para listar as propriedades disponíveis, que ainda são do banco. Você pode estudar como fazer isto.

## Ordem dos jogadores

Em nosso jogo, os participantes jogarão alternadamente, começando na ordem em que se inscreveram através da função `joinGame`. Isto é um acordo verbal, mas pode ser implementado no smart contract futuramente.

Ou... pode ser feito um sorteio do próximo jogador.

Qual você prefere implementar?

# Publicando em Blockchain

Para interagir com seus amigos e cada um utilizar a sua wallet, você precisa publicar o smart contract em um Blockchain "de verdade",ou seja, uma rede pública ou privada na qual todos tenham acesso.

Minha sugestão é começar experimentando uma Testnet, onde você não terá nenhum custo.

Algumas opções:

* Ehtereum 1.0: Ropsten ou Rinkeby
* RSK: Testnet

Para isto será necessário criar uma carteira web, por exemplo, [Metamask](https://metamask.io/) e configurar o Remix para utilizá-la.

Caso queira publicar na Testnet da RSK, o tutorial [crie seu primeiro smart contract utilizando Remix e Metamask com a RSK testnet](/2020/2020-03-27-Rsk-RemixMetamask/) ensina passo-a-passo como fazer isto. 

# Considerações finais

O projeto `Blockopoly` foi inspirado em uma excelente iniciativa da Microsoft: [Reactor](https://developer.microsoft.com/en-us/reactor/). São espaços espalhados pelo mundo onde os profissionais experimentam tecnologias líderes da indústria na Microsoft, parceiros e comunidades de código aberto, enquanto se encontram, aprendem e criam conexões.

Na [parte 1](/2020/blockopoly-01/) você conheceu a arquitetura do projeto e o primeiro smart contract: `Bank`, que controla o dinheiro, os saldos de cada um, a emissão e transferências.

Na [parte 2](/2020/blockopoly-02/) foi ensinado como criar o smart contract `AssetManager`, nosso gerenciador de ativos que é o administrador das propriedades negociadas. 

Nesta terceira e última parte do tutorial criamos o "coração" do projeto que é o smart contract `Blockopoly`, onde são definidos jogadores, propriedades negociadas, início, final do jogo e ganhador. Além disto demonstramos o funcionamento de uma partida.

Espero que esse tutorial tenha sido útil e agradeço caso tenha algum feedback para mim. Compartilhe o artigo caso tenha gostado :)

> Aguarde um vídeo sobre o assunto em meu canal: <a href="https://www.youtube.com/user/solangegueiros" target="_blank"> youtube Solange Gueiros</a>. Se quiser ser avisado quando a publicação acontecer é só assinar o canal.
