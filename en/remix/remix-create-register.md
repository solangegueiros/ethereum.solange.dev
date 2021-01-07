## Creating the smart contract Register

Click on symbol `+` - create a new file.

![create a new file](../../images/remix/image-10.png)

File name: `Register.sol`

![filename Register.sol](../../images/remix/image-11.png)

Copy this smart contract:

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

Paste it into Remix, here:

![Paste register.sol at Remix](../../images/remix/image-12.png)

### Register.sol

This smart contract has:

* A variable `info` to store a string
* A function `getInfo()` to return the string stored at variable info
* A function `setInfo()` to change the string stored at variable info


