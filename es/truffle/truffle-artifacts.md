# Artefatos del smart contract

[truffle-artifacts-content](truffle-artifacts-content.md ':include')

Por ejemplo, echa un vistazo a `ABI` para el contrato inteligente `Register.sol`

![register json abi](../../images/truffle/image-20.png)

Y mira la sección `networks` del contrato inteligente `Register.sol` 

![register json networks](../../images/truffle/image-21.png)

Esto es register.sol:

```solidity
pragma solidity 0.5.4;

contract Register {
    string private info;

    function setInfo(string memory _info) public {
        info = _info;
    }
    
    function getInfo() public view returns (string memory) {
        return info;
    }
}
```

