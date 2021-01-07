### Artifacts

Para interactuar con un contrato inteligente publicado, necesitas 2 información:
1. ABI - Application Binary Interface
2. Contract address

Esta información es parte de los artefactos del smart contract.
La información del contrato publicado se almacena de forma predeterminada en la carpeta `build\contracts`.
Allí encontrará un archivo JSON con el mismo nombre de nuestro contrato inteligente.

La sección `ABI` - Application Binary Interface - contiene la forma estándar de interactuar con contratos en el ecosistema Ethereum, tanto desde fuera del Blockchain como para la interacción de contrato a contrato.
Source: [Solidity docs](https://docs.soliditylang.org/en/v0.7.5/abi-spec.html)

La sección `networks` contiene las redes en las que se publicó el contrato inteligente, incluida su dirección y el hash de la transacción.
