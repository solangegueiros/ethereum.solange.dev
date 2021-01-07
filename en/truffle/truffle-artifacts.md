# Artifacts for a smart contract

[truffle-artifacts-content](truffle-artifacts-content.md ':include')

For example, take a look at `ABI` for smart contract `Register.sol` 

![register json abi](../../images/truffle/image-20.png)

For example, take a look at `networks` for smart contract `Register.sol` 

![register json networks](../../images/truffle/image-21.png)

Take a loot at register.sol:

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

