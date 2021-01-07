
### No Truffle console

Se você já está executando o Truffle console conectado a uma rede, 
é só executar o comando `migrate`.

```shell
migrate
```

### No terminal, fora do console Truffle

Faremos isso executando os comandos abaixo diretamente no terminal,
sem usar o console Truffle, para mostrar essa alternativa.

Para usar uma rede específica previamente configurada no arquivo `truffle-config`,
você precisa especificar isso usando o parâmetro `- network`.

Por exemplo, farei isso na rede `myNetwork`.
Execute este comando em um terminal (não no console do Truffle):

```shell
truffle migrate --network myNetwork
```

