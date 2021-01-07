
Primeiro precisamos criar um novo arquivo com instruções para publicação. 
Ao encontrá-lo, Truffle vai processá-lo no momento do deploy.

O diretório `migrations` contém arquivos JavaScript que auxiliam a publicação de contratos no blockchain. 
Estes arquivos são responsáveis pelo preparo das tarefas de publicação 
e são escritos com base no pressuposto de que suas necessidades de implantação podem mudar com o tempo. 
O histórico das publicações executadas anteriormente é salvo no blockchain através de um smart contract especial criado automaticamente pelo Truffle, chamado Migrations. 
(source: [running migrations](https://www.trufflesuite.com/docs/truffle/getting-started/running-migrations))

Usualmente começamos o nome do arquivo com um número, dado que o Truffle faz o deploy dos arquivos em ordem alfabética e desta forma definimos a ordem de publicação dos smart contracts.
