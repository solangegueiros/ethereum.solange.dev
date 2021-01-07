# Artefatos do smart contract

[truffle-artifacts-content](truffle-artifacts-content.md ':include')

Por exemplo, dê uma olhada na  `ABI` para o smart contract `Register.sol` 

![register json abi](../../images/truffle/image-20.png)

E veja a parte `networks` do smart contract `Register.sol` 

![register json networks](../../images/truffle/image-21.png)

Veja o register.sol:

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

