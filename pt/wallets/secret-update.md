
Atualize seu mnemônico no arquivo `.secret`,
localizado na pasta do projeto e salve-o.

![update mnemonic](../../images/wallets/image-02.png)

Dê uma olhada no arquivo `truffle-config.js` para perceber que:
1. usamos `HDWalletProvider`
2. carregamos o mnemônico do arquivo `.secret`.

![truffle-config HDWalletProvider mnemonic](../../images/wallets/image-03.png)
