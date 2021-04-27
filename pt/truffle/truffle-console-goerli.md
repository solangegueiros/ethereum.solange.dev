### Gorli no arquivo Truffle config

Dê uma olhada no arquivo `truffle-config.js`, 
na seção `network`, 
Görli testnet está configurada utilizando o HDWalletProvider e o mnemonic.

![truffle-config HDWalletProvider mnemonic](../../images/truffle/image-08.png)

Talvez sua configuração não seja exatamente esta, foram realizadas algumas atualizações na conexão, mas você verá as configurações para a rede Goerli.

### Conectando a Gorli testnet

Execute o console de desenvolvimento para esta rede.

```shell
truffle console --network goerli
```

![truffle console network goerli](../../images/truffle/image-09.png)
