### Artifacts

To interact with a published smart contract, you need to have 2 informations:
1. ABI - Application Binary Interface
2. Contract address

This information are part of the smart contract's artifacts. 
The published contract information is stored by default in the `build\contracts` folder. 
Over there you will find a JSON file with the same name of our smart contract.

The section `ABI` - Application Binary Interface - contains the standard way to interact with contracts in the Ethereum ecosystem, both from outside the blockchain and for contract-to-contract interaction. 
Source: [Solidity docs](https://docs.soliditylang.org/en/v0.7.5/abi-spec.html)

The section `networks` contains the networks in which the smart contract was published, including its address and hash of the transaction.
