## Criando o smart contract Register

Clique no símbolo `+` - create a new file - para criar um arquivo novo.

![create a new file](../../images/remix/image-10.png)

Nome do arquivo / file name: `Register.sol`

![filename Register.sol](../../images/remix/image-11.png)

Copie o smart contract abaixo:

```solidity
pragma solidity 0.5.4;

contract Register {
    string private info;
    
    function getInfo() public view returns (string memory) {
        return info;
    }
    
    function setInfo(string memory _info) public {
        info = _info;
    }
}
```

Ou deste 
[Register.sol gist](https://gist.github.com/solangegueiros/6f30100662f8583ea39a49a5fa198b89)

Cole no Remix:

![Paste register.sol at Remix](../../images/remix/image-12.png)

### Register.sol

Este smart contract tem:

* Uma variável `info`, privada, para armazenar uma string
* Uma função `getInfo()` para retornar a string armazenada na variável `info`
* Uma função `setInfo()` para alterar a string armazenada na variável `info`

### Remix Images

D:\BLOCKCHAIN\SOLANGE.DEV\GITHUB\solange.dev\content\blog\2020\blockopoly-01\images

