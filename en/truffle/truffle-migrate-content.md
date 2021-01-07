
### Inside of development console

If you are already running the Truffle console connected to a network, 
you only need to execute the command `migrate`.

```shell
migrate
```

### Outside of development console

We will do it running the below command directly in the terminal, 
without using the Truffle console, to show you this alternative. 

To use an especific network previously set up on `truffle-config` file, 
you need to specify this using the parameter `-- network`.

For example, I will do it on the network `myNetwork`.
Run this command in a terminal (not in Truffle console):

```shell
truffle migrate --network myNetwork
```

