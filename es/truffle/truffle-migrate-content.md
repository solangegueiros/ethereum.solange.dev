
### Dentro de la consola Truffle

Si ya está ejecutando la consola Truffle conectada a una red,
solo necesitas ejecutar el comando
 `migrate`.

```shell
migrate
```

### Fuera de la consola Truffle

Lo haremos ejecutando lo siguiente comando directamente en la terminal,
sin usar la consola Truffle, para mostrarte esta alternativa.

Para utilizar una red específica configurada previamente en el archivo `truffle-config`,
necesita especificar esto usando el parámetro `- network`.

Por ejemplo, lo haré en la red `myNetwork`.
Ejecute este comando en una terminal (no en la consola Truffle):

```shell
truffle migrate --network myNetwork
```

