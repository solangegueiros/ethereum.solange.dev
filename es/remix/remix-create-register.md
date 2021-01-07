## Creando el contrato inteligente Register

Haz clic en el símbolo `+` - create a new file - para crear un archivo nuevo.

![create a new file](../../images/remix/image-10.png)

Nombre del archivo / file name: `Register.sol`

![filename Register.sol](../../images/remix/image-11.png)

Copie el contrato inteligente a continuación:

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

Y pégalo aquí:

![Paste register.sol at Remix](../../images/remix/image-12.png)

### Register.sol

Este contrato inteligente tiene:

* Una variable `info` para almacenar una string
* Una función `getInfo()` para devolver la string almacenada en la variable `info`
* Una función `setInfo()` para cambiar la string almacenada en la variable `info`



