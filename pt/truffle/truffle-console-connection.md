
Em qualquer rede, execute estes comandos no console do Truffle:

### Block number

Apresenta o número do último bloco minerado.

```javascript
(await web3.eth.getBlockNumber()).toString()
```

### Network ID

Para saber o ID da rede, execute este comando:

```javascript
(await web3.eth.net.getId()).toString()
```

> [!TIP]
> Görli testnet network ID: 5

Confira as últimas etapas nesta figura:

![connect to rsk network](../../images/truffle/image-11.png)

Você deve ter percebido que eu executei o comando getBlockNumber duas vezes e o número do bloco aumentou, 
então concluímos que a conexão está ok
:smile:
