### Gorli in Truffle config file

Take a look at the `truffle-config.js` file, 
in the `network` section, 
Görli testnet is configured using HDWalletProvider and the mnemonic.

![truffle-config HDWalletProvider mnemonic](../../images/truffle/image-08.png)

Perhaps your configuration is not exactly this, some updates have been made to the connection, but you will see some settings for the Goerli network.

### Connect to Gorli testnet

Run the development console for this network.

```shell
truffle console --network goerli
```

![truffle console network goerli](../../images/truffle/image-09.png)

