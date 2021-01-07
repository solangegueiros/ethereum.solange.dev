
To deploy a smart contract using Truffle, 
we need a new migrations file where Truffle will find it. 
This file contains instructions to deploy the smart contract. 

The `migrations` folder has JavaScript files that help you deploy contracts to the network. 
These files are responsible for staging your deployment tasks, 
and they're written under the assumption that your deployment needs will change over time. 
A history of previously run migrations is recorded on-chain through a special Migrations contract. 
(source: [truffle: running-migrations](https://www.trufflesuite.com/docs/truffle/getting-started/running-migrations))

We usually start the file name with a number, 
since Truffle deploys the files in alphabetical order 
and in this way we define the order of publication of the smart contracts.

