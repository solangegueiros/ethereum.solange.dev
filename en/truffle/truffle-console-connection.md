
On any network, run this commands in the Truffle console:

### Block number

Shows the last block number.

```javascript
(await web3.eth.getBlockNumber()).toString()
```

### Network ID

To get the network ID, run this command:

```javascript
(await web3.eth.net.getId()).toString()
```

> [!TIP]
> Görli testnet network ID: 5

Check it out the last steps in this image:

![connect to rsk network](../../images/truffle/image-11.png)

You just realized that I got the last block twice, and the block number increased, so we conclude that the connection is ok 
:smile:
