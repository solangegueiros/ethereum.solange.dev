### Gorli en el archivo Truffle config

Mira el archivo `truffle-config.js`, 
en la sección `red`,
Görli testnet se configura usando el HDWalletProvider mediante el mnemónico.

![truffle-config HDWalletProvider mnemonic](../../images/truffle/image-08.png)

Es posible que su configuración no sea exactamente esta, se han realizado algunas actualizaciones en la conexión, pero verá algunas configuraciones para la red Goerli.

### Conexión a la  Gorli testnet

Ejecute la consola de desarrollo para esta red.

```shell
truffle console --network goerli
```

![truffle console network goerli](../../images/truffle/image-09.png)

