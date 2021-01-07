### Artifacts

Para interagir com um smart contract, precisamos saber 2 coisas:
1. ABI
2. Endereço

Essas informações fazem parte dos artefatos do smart contract.
As informações do contrato publicado são armazenadas por padrão na pasta `build\contracts`.
Você encontrará um arquivo JSON com o mesmo nome do contrato inteligente.

A seção `ABI` - Application Binary Interface - contém o padrão para interagir com contratos no ecossistema Ethereum, tanto de fora do Blockchain quanto para interação de um contrato a outro.
Fonte: [Solidity docs](https://docs.soliditylang.org/en/v0.7.5/abi-spec.html) (em inglês)

A seção `networks` contém as redes nas quais o smart contract já foi publicado, incluindo seu endereço e o hash da transação.
