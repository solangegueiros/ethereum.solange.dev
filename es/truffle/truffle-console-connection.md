
En cualquier red, ejecute estos comandos en la consola Truffle:

### Block number

Muestra el último número de bloque.

```javascript
(await web3.eth.getBlockNumber()).toString()
```

### Network ID

Para obtener la identificación de la red, ejecute este comando:

```javascript
(await web3.eth.net.getId()).toString()
```

> [!TIP]
> Görli testnet network ID: 5

Mira los últimos pasos en esta imagen:

![connect to rsk network](../../images/truffle/image-11.png)

Te acabas de dar cuenta de que obtuve el último bloque dos veces y el número de bloque aumentó, 
por lo que concluimos que la conexión está bien.
:smile:
