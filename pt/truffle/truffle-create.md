# Criando um projeto com Truffle

Há duas opções para inicializar um projeto:

1. Um modelo de projeto vazio
2. Um projeto baseado em um Truffle Box

## 1 - Inicialize um novo projeto Truffle 

Crie um novo diretório, `myproject`, por exemplo, e vá para a pasta no terminal.

```shell
mkdir myproject
cd myproject
```

Por exemplo, eu vou criar em `C:\ETH\` (Estou utilizando Windows).

Meu projeto estará localizado no diretório `C:\ETH\myproject`.

![myproject folder](../../images/truffle/image-08.png)

Na pasta do seu projeto, inicialize um projeto Truffle:

```shell
truffle init
```

![truffle init](../../images/truffle/image-09.png)

Abra a pasta no VSCode. 
Você verá uma estrutura de diretórios como esta:

![truffle file structure](../../images/truffle/image-11.png)

* `./contracts`: Todos os smart contracts serão salvos nesta pasta.
* `./migrations`: Os scripts para publicação ficarão armazenados aqui.
* `./test`: Aqui serão salvos os scripts para testes.
* `./truffle-config.js`: Este é o arquivo de configuração do Truffle. Aqui vamos configurar as redes, incluindo RSK.

Veja que os seguintes arquivos também foram criados:

* `Migrations.sol`: Smart contract que registra todos as publicações realizadas em uma rede.
* `1_initial_migration.js`: Publicação do `Migrations.sol`.

### Inicialize um projeto npm

Quando inicializamos um projeto Truffle a partir do template, também precisamos inicializar um projeto npm.

Para inicializar um projeto npm na pasta `myproject`,  execute o comando abaixo no terminal:

```shell
npm init -y
```

![npm init](../../images/truffle/image-12.png)

## 2 - Inicialize um projeto baseado em um Truffle Box

> [!WARNING]
> Você só precisa fazer esta parte se não escolheu a opção 1.

Truffle Boxes são modelos. 
Além dos arquivos do Truffle, 
Truffle Boxes podem conter outros módulos úteis, como smart contracts Solidity, bibliotecas, páginas front-end e mais.

Na opção 1, quando usamos `truffle init`, estamos utilizando um tipo especial de Truffle box. 

Para criar um projeto a partir de uma Truffle Box,
vá para (pt/truffle/truffle-boxes.md) 

:sun_with_face:
